# IQ Decision Workbench — technical specification

**Status:** proposed implementation baseline, 28 September 2026. Read [Product specification](PRODUCT-SPEC.md) and [IDE handover](IDE-HANDOVER.md). Field names, module boundaries, runtime choices and operation names below are design proposals, not assertions that these APIs already exist. The IDE lead may refine them while preserving the intended behaviour and recording material changes.

## 1. Architecture

The default direction is a provider-neutral semantic model with a deterministic core and replaceable presentation/assessment adapters:

```text
User / IQ Wealth / other authorised agent
                 |
       checked authoring operations
                 |
    framework + case + evidence records
                 |
         validate and normalise
                 |
         immutable input snapshot
          /                 
 optional assessment adapter    structured observations / manual inputs
          \                 /
       typed, evidence-bound inputs
                 |
       pure deterministic evaluator
                 |
      evaluation result + rule trace
          /                 
   browser renderer       records / exports

Separate optional orchestration:
source retrieval -> observation update -> evaluation -> notification
```

The evaluator does not fetch data, call an LLM, read the current wall clock implicitly, save files or execute actions. Its dependencies are explicit. The browser and a later scheduled runner use the same evaluator, not independent translations of the rules.

Use a normal browser with a loopback host for local records. The starting preference is a small maintainable JavaScript/TypeScript implementation compatible with the existing repository. Whether to reuse the earlier dependency-free pilot, use an Archify adapter, or add a dedicated decision renderer is an implementation decision after a bounded compatibility review. Do not force interactive controls into the existing schema by pretending they are already supported.

## 2. Reviewed baseline and reuse decisions

At the reviewed `main` commit `307fc4b353e75eb23d620c727891515955fa3aa3`:

| Asset | Verified role | Implication |
|---|---|---|
| `docs/interactive-decision-workbench-experiment.md` | Product/architecture lessons and candidate node vocabulary | Preserve these lessons; it is not an implemented generic runtime contract. |
| `experiments/interactive-decision-workbench/examples/investment-node-controls.html` | Standalone hard-coded HTML/JavaScript interaction prototype | Reuse interaction ideas, not a claim that the JSON examples already drive it. |
| `conditional-decision.json` | Pre-entry semantic example | Useful seed; lacks full provenance/unknown/versioned runtime semantics. |
| `position-review.json` | Separate live-position example and hard-condition precedence | Preserve lifecycle distinctions; the illustrated drift points have no defined measurement method. |
| `examples/investment-decision.architecture.json` | Conventional Archify process map | Remains valid as a process explanation independently of this workbench. |
| `archify/package.json` | Version 2.15.0; architecture/workflow/sequence/dataflow/lifecycle renderers; Node >=18 declared | Do not claim a sixth native decision type exists. Avoid incidental runtime upgrades until needed. |
| `archify/SKILL.md` | Instructions for generating and delivering ordinary diagram artefacts | Its per-artefact freeze/repair and single-screen rules are not a blanket ban on developing a new interactive product. |

The earlier 14 September 0.1.0 pilot is separately documented in the user's Library. Its report claims 69 Node tests and 28 Chromium checks using an injected harness; installed Windows/IQ Browser/native navigation were not accepted end to end. Only its skill/report were reviewed here, not its code. Reuse should be based on actual compatible code and test results, not on those counts alone.

The fork is public and Issues were disabled at review. Use repository documents for this handover; do not enable Issues, change visibility or publish client artefacts just to support the plan.

## 3. Proposed module boundaries

| Module | Responsibility |
|---|---|
| Contracts/schema | Versioned data shapes, discriminated node types, input constraints and structured diagnostics |
| Templates | Reusable definitions, educational content, compatibility rules, fixtures and migrations |
| Evaluator | Pure calculations, applicability, dependency ordering, logical composition, precedence and trace |
| Store | Case/evidence persistence, revision compare-and-swap, history, operation idempotency and recovery |
| Assessment adapters | Optional provider calls and strict conversion to a provider-neutral assessment record |
| Application service | Combines validated operations, persistence and optional assessments; implements existing permissions |
| Renderer | Node controls, graph layout, inspector, scenarios, comparisons, history and accessible linear view |
| Agent bridge | Discoverable contracts and operations for case authoring, evidence updates, scenarios and evaluation |
| Export | Explicit working-record, scenario, sanitised-template and static-snapshot formats |
| Monitoring adapter | Later source polling/events, scheduling, deduplication and notifications through existing orchestration |

Keep these logical boundaries even if the initial implementation uses a few files rather than a package per row. Do not build a microservice estate for a local pilot.

## 4. Semantic object model

### 4.1 TemplatePackage / FrameworkDefinition

A template package carries a stable ID, version, title, purpose, supported lifecycle/instrument scope, education references, framework definition, fixtures and declared module requirements.

The framework includes node definitions, entry points, dependency/control relationships, outcome rules, applicability conditions and any calculation/assessment contracts. Layout hints are semantic (stage, group, preferred reading order), not model-authored pixel coordinates.

A case pins a framework version or a complete versioned local framework snapshot. Updating a template catalogue does not retroactively change existing cases. A user-specific adaptation creates a revised framework/overlay with its parent identified. Labels can change without pretending the meaning is unchanged; material semantic changes require a new revision/fingerprint.

### 4.2 CaseRecord

Candidate fields:

| Field family | Required meaning |
|---|---|
| Identity | Case ID, title, schema version, framework ID/version, revision and content hash |
| Decision frame | Question, objective, alternatives, instrument/portfolio scope, horizon, currency and return basis |
| Lifecycle | Pre-entry, live-position or closed/review context, with origin of the lifecycle fact |
| Inputs | Typed material values, each linked to its datum/provenance record |
| Policies | Explicit constraints and their authorisation/source, distinguishable from observations |
| Evidence | References to relevant evidence records and assessment results |
| State dates | Created, saved, reviewed and relevant valuation/as-of dates, not one ambiguous timestamp |
| User disposition | User's stated choice and notes, independent of a graph outcome or transaction |
| Relations | Related cases, shared capital scope, prior cases and review relationships |
| Classification | Real or synthetic; privacy/export scope |

New real cases should not inherit populated demo facts. Defaults that are merely display preferences are different from defaults that manufacture an investment assumption.

### 4.3 Datum and provenance

Every material input has a typed value or explicit absence. Use a representation that preserves `false`, `0`, empty text and missing as different states. For a numeric field, blank is missing, not a request to coerce `Number('')` to zero.

Useful provenance categories: observation, user statement, estimate, assumption, policy, human assessment, model assessment and derived result. Record who/what supplied the value, source IDs, relevant dates, method and limitations. A model using a user-provided assumption does not turn it into an independently verified fact.

Represent unit, currency, horizon, valuation basis, gross/net basis and portfolio denominator where relevant. Dates should use unambiguous machine timestamps plus display timezone/context. Preserve precision needed for calculations separately from display formatting.

Avoid a single catch-all confidence number. Data freshness, source reliability, estimate range, semantic-model distribution and investment-outcome probability are different concepts.

### 4.4 EvidenceRecord

Record source identity/location, document/version or snapshot hash when available, relevant passage/table reference, author/publisher if known, published/effective/as-of time and retrieved time. Include scope and any extraction/transformation method. Retain contradictions and superseding versions.

A link is not the same as a stored point-in-time snapshot. An unavailable or mutable source may limit reproducibility; say so in the evaluation receipt. Do not describe an excerpt as the entire document. Respect source access and redistribution constraints when exporting.

Source content is untrusted data, not instructions. Text such as “ignore this limit” inside a retrieved announcement cannot edit a policy or grant tool permissions.

### 4.5 AssessmentRecord

Record the question-contract ID/version/fingerprint, exact evidence/input snapshot identities, provider/model identity, request/response dates, answer type, validated answer and any returned probability/distribution fields. Retain raw provider output where appropriate with credentials and unnecessary personal data removed.

Status is separate: proposed, accepted under a configured policy, superseded, abstained, invalid response, service failure, cancelled or stale relative to current inputs.

An assessment cannot be applied to a different case revision/evidence version just because it concerns the same ticker. A later-arriving response to old evidence is retained as historical/proposed or discarded according to a documented rule; it does not replace current state silently.

### 4.6 ScenarioRecord

Record scenario ID/name, base case revision/hash, a typed set of overrides, rationale, synthetic status, creator and timestamps. Overrides retain whether they change assumptions, observations for a hypothetical world, or policy what-ifs.

A scenario does not change durable policy merely because the browser displays it. Applying a scenario uses expected-base revision checking and the user's current authorisation. Keep selected changes explicit, not a blind replacement of the entire case.

### 4.7 EvaluationResult

Record case/framework/schema/evaluator identities, input snapshot/hash, assessment references and an explicit evaluation clock. Return overall outcome code, per-node evaluation, applied route(s), decisive reasons, unresolved conditions, stale/conflicting inputs, calculations and diagnostics.

The trace explains declared rules and source dependencies; it is not a purported reconstruction of hidden model reasoning. Store human-readable explanation templates alongside stable reason codes so the main outcome can be explained without an LLM.

## 5. Node vocabulary

Start with a small validated set, adding a type only when a real template needs it:

| Kind | Inputs and behaviour |
|---|---|
| `information` | Text/evidence context; not automatically a decision gate |
| `yes_no` | Boolean or explicit unknown; meaningful yes/no branches; no default true for missing evidence |
| `number_compare` | Compatible left/right operands, explicit operator, precision policy and units |
| `choice` | Declared options with stable IDs; includes no-match/unresolved where appropriate |
| `range` | Declared scale/unit and inclusive/exclusive boundaries; not an unexplained AI score |
| `calculation` | Registered deterministic module and validated operands, not arbitrary executable expressions |
| `group` | Explicit composition such as all/any, only when the supported version defines its semantics |
| `outcome` | A rule result with code/meaning; not a capability to execute a transaction |

A scenario-expectancy module can supply the earlier pilot's fourth template without opening arbitrary formulas. For the first slice, an all-required-gates model is acceptable. If broader composition is not implemented, validation must reject unsupported group kinds rather than approximate them.

Nodes also carry stage/group, label, purpose, education ID, operand/evidence references, applicability, role (information, hard constraint, review trigger, preference), and output relationships. Keep role distinct from predicate truth.

## 6. Four-state logic plus separate applicability

For an applicable condition, use explicit logical results:

| State | Meaning |
|---|---|
| True / matched | The declared predicate is satisfied with eligible inputs |
| False / not matched | The predicate is not satisfied with eligible inputs |
| Unknown | Needed information is absent, unresolved, disputed or ineligible under freshness rules |
| Error | The condition cannot validly be evaluated, such as incompatible units or an invalid definition |

Applicability is independent: applicable, not applicable, or not yet determined. Execution/trace status can additionally distinguish evaluated from intentionally skipped. A skipped downstream condition must not be shown as passing.

For Boolean groups, use explicit truth tables. For valid `all`, any known false makes the predicate false; otherwise unknown inputs leave it unknown; all true gives true. For valid `any`, any known true gives true; otherwise unknown inputs leave it unknown; all false gives false. Errors are retained in diagnostics and may block the affected outcome even if an unrelated Boolean result is already known. Define outcome eligibility separately from predicate truth so a decisive fact and incomplete coverage can both be reported.

Do not multiply independent-looking Jev probabilities as though the questions' answers were statistically independent. Parallel execution is not independence of the underlying evidence.

## 7. Graph semantics and evaluation order

Distinguish four relationship types:

- **Dependency:** a value/result is needed to compute another node.
- **Control:** an explicitly declared condition routes to a possible next step/outcome.
- **Evidence:** a source supports or challenges a claim/assessment.
- **Review:** a conceptual return to research after a later event, not an executable cycle in one evaluation.

Initial executable dependencies/control flow should be acyclic and bounded. Cycles in review relationships may be displayed but cannot recursively trigger themselves. A future iterative/simulation module needs its own termination/convergence contract.

Validate stable unique IDs, reference existence, node-type compatibility, entry points, outcome reachability, applicable branches and deterministic ordering. Unreachable required nodes, ambiguous competing outcomes and unsatisfied module dependencies need actionable diagnostics.

The prototype's HTML and JSON do not currently have identical execution traces: the HTML computes return and fit together while the sample JSON can route from a failed return hurdle directly to watch. The implemented product must choose explicit semantics and use one evaluator for both the path display and outcome. It may compute independent conditions for information while labelling which ones were decisive or on the selected route.

Do not short-circuit away independent hard conditions merely because an earlier display path appears favourable. Collect all required hard-condition assessments for the relevant lifecycle before selecting a reassuring outcome.

## 8. Outcome precedence and lifecycle

### 8.1 Valid pre-entry case

1. Invalid required structure prevents a new authoritative evaluation; show diagnostics.
2. A known failed hard constraint yields “configured constraint not satisfied,” with other unknown/error conditions still visible.
3. Required unresolved conditions prevent a claim that entry conditions are satisfied.
4. If all required applicable conditions are satisfied with eligible inputs, report exactly that.
5. Any implementation planning/disposition is a separate operation.

### 8.2 Valid live-position case

1. A confirmed applicable hard-condition match takes precedence over softer review results, even when unrelated softer inputs are missing.
2. A known hard-condition result with other unresolved hard inputs should report both the confirmed trigger and incomplete remaining coverage; do not hide the trigger.
3. Without a known trigger, unresolved required hard-condition evidence prevents “no review needed.”
4. Known softer review triggers produce review status; other missing conditions remain visible.
5. Only complete eligible required checks can support “no configured trigger detected as of this snapshot.” This is not a recommendation to hold indefinitely.

A structurally invalid document is different from a valid case with a missing datum. On invalid new state, show the validation failure and any last valid result clearly marked historical, not silently current. Do not erase a recorded hard-trigger event because a subsequent input file becomes corrupt.

### 8.3 Closed/review case

Use historical snapshots and the recorded lifecycle. Do not issue fresh entry or exit implications merely because present-day data has been attached to a historical case. A reopened evaluation is an explicit new revision/context.

Node colours derive from role and effect, not simply true/false. A matched risk-breach condition can be adverse; a false review-trigger condition can be benign only when the relevant required checks are complete.

## 9. Numerical and financial-domain contracts

### 9.1 Numeric representation

Reject non-finite numbers and invalid numeric strings. Declare supported precision and comparison policy. Prefer a representation/module suited to the domain (for example integer minor currency units or an explicit decimal implementation where necessary). Never round for display before evaluating a threshold.

Operators `>`, `>=`, `<`, `<=`, equality and ranges have explicit boundary semantics. An equality tolerance must be declared for that metric, not introduced silently to manufacture a match.

### 9.2 Comparability

Before comparison, check units, currencies, horizons, annualised versus holding-period basis, gross/net convention and relevant denominator. A conversion requires an identified transformation and source when market-dependent. Missing currency/horizon is not permission to assume compatibility.

For portfolio exposure, record funding source, total-value basis and valuation date. For capital shared between cases, maintain at least a warning/relation identifying competing uses; do not sum independent favourable cases into an executable portfolio without aggregate evaluation.

### 9.3 Scenario expectancy

For explicit probabilities p_i and compatible payoffs r_i, compute expected payoff as the sum of p_i times r_i. Where costs vary by scenario, compute the sum of p_i times (r_i minus c_i). A separate common cost may be subtracted once only if the contract states it has not already been included.

Probabilities must be supplied with a basis, lie in range and sum to one within the declared small tolerance. Reject negative or missing probabilities. No automatic normalisation. Explicitly identify whether scenarios are assumed exhaustive and mutually exclusive.

Retain probabilities, assumptions, costs and output precision in the receipt. A mean is not a downside-risk summary or a geometric compound return. Do not infer repeated-trade independence, annualisation or compounding without an explicit module.

### 9.4 Risk/sizing extension

A supported long-only sizing example may calculate units from a risk budget and assumed per-unit loss, but that assumed loss is not a guaranteed worst case. Fees, minimum lots, currency conversion, liquidity/gaps and instrument limitations belong to the module contract. Short, leveraged and option cases require appropriate modules rather than reusing the long-only formula unmodified.

A future simulation module records model version, input distribution/dependence, seed, sample count, convergence diagnostics and limitations. A seeded simulation remains conditional on its model and inputs.

## 10. Freshness, contradictions and evidence eligibility

Use an explicit evaluation time and per-input/source freshness policy where material. Retrieval time does not replace a source's effective or as-of time. Reopening a case or rerunning a model does not refresh its market evidence.

Separate historical usefulness from current eligibility: an old statement can remain valid evidence of the original thesis while being inadequate for a current quote check. Mark stale data visibly; whether it blocks a particular condition depends on the declared role/policy.

Conflicting material sources should remain available with a resolution or unresolved status. A chosen source can be recorded with rationale; never overwrite the conflicting observation as though it never existed.

## 11. Browser state and persistence

Maintain distinct layers:

1. Saved, versioned case state.
2. Loaded baseline snapshot used by the current browser session.
3. Unsaved what-if overrides.
4. Derived evaluation for the displayed combination.
5. Viewer-only state such as zoom, focus and expanded evidence.

File refresh must not overwrite dirty scenario inputs. Show “saved source changed” with an inspect/rebase/reload option. A conflicting scenario apply should return the changed fields and expected/current revisions, not blindly discard the user's work.

Use atomic validated writes with revision/hash compare-and-swap enforced inside the actual write critical section. A check followed by an unprotected later write is not sufficient. Preserve history or another recoverable previous revision and increment revisions consistently. Include operation IDs to prevent duplicate writes on retry.

An interrupted save must leave either the complete previous revision or the complete new revision, not partial JSON. Corrupt files should remain inspectable/recoverable and must not be silently replaced with a demo/default case.

For the first pilot, a read-only local HTTP API plus checked agent/CLI writes is acceptable and matches the earlier pilot direction. A richer browser save bridge can be added if needed, retaining scoped write permissions, validation and conflict handling. API names are open; behaviour is not.

## 12. Agent-facing operations

Expose a concise discoverable contract. Proposed operations, not existing commands:

| Operation | Behaviour |
|---|---|
| Describe capabilities/templates | Reports actual supported node kinds, modules, versions and available integrations |
| Create case | Uses a selected compatible template; unknown material defaults; refuses accidental overwrite |
| Read case / evidence / evaluation | Returns exact IDs/revisions and relevant scope |
| Prepare proposed update | Produces a candidate based on an exact revision/hash |
| Validate candidate | Returns machine-readable errors/warnings with paths and understandable repairs |
| Apply typed update | Validated, authorised and conflict-checked; policy/lifecycle changes distinguishable from observations |
| Evaluate | Pure evaluation of an explicit snapshot/time |
| Create/export/apply scenario | Preserves base revision and selected overrides |
| Read visible scenario | Only when an actual bridge exposes the current browser state; otherwise use an exported scenario |
| Request assessment | Calls configured provider only for the stated evidence/question contract |
| Export / restore history | Produces explicit formats; restore is a new recoverable revision |

Do not put global “ask first” gates in front of every operation. Use the user's task, standing instructions and existing tool authority. Distinguish routine reversible work from a genuinely new policy/lifecycle decision, sensitive disclosure, paid deployment or external side effect. The development lead's ability to improve code and templates must not be confused with a client assistant's right to rewrite a client's policy during routine evidence updates.

A reported save must include a read-back or authoritative result identifying the saved revision. An assistant must not claim knowledge of unsaved browser controls from a disk file that does not contain them.

## 13. Optional semantic assessment contract

### 13.1 Input preparation

Keep the question's meaning complete in instructions and criteria; an internal node/question ID is not sufficient context. Send only the relevant evidence, identities, previous comparison state and permissible outcomes. Preserve provenance and label untrusted text.

Construct exact candidates in code where possible. The model cannot select a missing candidate; include a no-match/insufficient-evidence outcome and check coverage. Do not reduce several distinct questions to “is this investment good?”

### 13.2 Provider-neutral answer types

Support a bounded choice, a yes/no probability assessment and a rubric-based score only where their semantics fit. Preserve returned probability/distribution fields without relabelling them as investment probabilities.

Official TypeSafe guidance states that independent questions in one request cannot see each other's answers. Batch independent questions over the same state; issue a subsequent request when an earlier result is needed to fetch new evidence or construct options. Extra questions still consume request budget.

For Choice/Score, distribution concentration is not overall correctness. A yes/no probability near one-half is not medium severity. Score levels need meaningful defined anchors. Do not invent a confidence field for a primitive that does not supply one.

### 13.3 Consumption policy

Initial live integration should run on a narrow evidence-comparison question, with deterministic fixtures and optional shadow evaluation. Promotion from proposed assessment to a consumed input is controlled by a recorded policy and existing user direction. Low-consequence repeated assessments can be auto-consumed after configuration; do not require a click for every routine sample.

Unknown, ambiguous, malformed or failed provider responses leave the relevant input unresolved and visible. They do not disable unrelated manual/deterministic work or force a false value. An available main agent/user can resolve the question without treating the provider failure as a platform-wide blocker.

### 13.4 Validation and cache identity

Validate expected question keys, answer type, declared choice IDs, finite/ranged numerical fields and probability totals where the API supplies a distribution. Treat the exact installed SDK/API as authoritative rather than coding against remembered payloads.

Cache identity includes tenant/case scope where applicable, evidence/input fingerprint, question semantics/version, provider/model identity and relevant normalisation settings. Rule-evaluation caches also include framework/evaluator version, policies and evaluation time/freshness inputs. Changing display weights alone need not rerun unchanged underlying assessments, but changing a question or evidence does.

Cancel or quarantine stale in-flight responses after relevant edits. Debounce interaction-driven requests; do not call Jev on every slider movement for deterministic inputs. Log actual latency/cost when available, not demo claims.

### 13.5 Evaluation of the model feature

Use representative labelled examples, including paraphrases, negation, missing dates, changed scope, contradictions, no-match cases and adversarial source text. Keep calibration/development examples separate from holdout examples. Track false material-change flags, missed material changes, abstention, malformed responses, latency and correction rates. Choose thresholds for the task/consequence; no universal 0.90 threshold is specified here.

Mock-provider tests verify application plumbing only. Label them as mock and do not claim model accuracy from them.

## 14. Renderer and interaction requirements

Use real HTML controls with labels, keyboard focus and sufficient target size. Prefer measured DOM/HTML node layout and a deliberate connection layer over brittle SVG `foreignObject` insertion. Framework-specific implementation is open.

Recompute layout after text/evidence expansion and viewport/font changes. Ensure connections do not cross unrelated opaque nodes and labels remain legible. Preserve stable positions where possible so a value update does not reorganise the entire diagram.

Controls should be discoverable inside nodes. Expanding education or evidence must not cause hidden inputs or unexplained scroll jumps. Make active/scenario/unknown/stale/error states distinct through text and styling, not colour alone.

Provide dark/light themes and reduced-motion behaviour. A contained, readable canvas scroller is acceptable for this workbench; upstream static-diagram single-screen rules do not automatically apply. The surrounding page should remain usable without uncontrolled whole-page horizontal overflow.

The renderer consumes EvaluationResult and node definitions. It does not reimplement business rules in event handlers. Scenario recomputation and saved-state recomputation follow the same evaluator.

## 15. Diagnostic and recovery contract

Useful stable diagnostic categories include:

| Category | Expected behaviour |
|---|---|
| Unsupported schema/node/module | Identify exact version/kind and preserve the record; do not approximate |
| Broken reference/cycle | Name the nodes/relationship and explain why evaluation cannot proceed |
| Missing required input | Show unresolved condition and relevant next work, not a fabricated value |
| Incompatible units/horizon/basis | Identify both sides and required conversion/clarification |
| Stale/conflicting evidence | Preserve source history and indicate effect on eligibility |
| Invalid probability distribution | Identify missing/out-of-range inputs or incorrect total |
| Revision conflict | Preserve both candidate and current state; require reread/reconciliation |
| Corrupt record | Expose readable diagnostic and recoverable history without default replacement |
| Assessment unavailable/invalid/stale | Mark that assessment unavailable; retain functioning local work |
| Export capability absent | Offer supported format and state what is excluded |

These should be domain-language messages for users with machine-readable details for agents. A validation failure is useful feedback, not a generic reason for an IDE agent to abandon the task.

## 16. Local host and security posture

Bind to loopback by default. Limit accessible files to the selected workspace and known application assets; canonicalise paths and handle symlinks/traversal deliberately. Validate Host/origin and capability scope appropriate to the local host, and avoid treating loopback alone as authorisation. Do not expose a write endpoint without a scoped write design.

Keep provider credentials outside case JSON, static exports and browser bundles. Minimise data sent to providers and honour existing connection permissions. A schema-valid source URL is not automatically approved for unrestricted server-side fetching; source adapters need their own allowed-source and network boundary.

Escape/sanitise untrusted labels and evidence. Do not execute arbitrary source HTML, model-generated code, formulas, file paths or actions from decision JSON. Do not infer tool authority from a diagram node named “implement.”

Avoid client content in public Git commits, logs, screenshots and test fixtures. Synthetic data is the default for development. A content hash supports integrity/reproducibility but is not an authorship signature or proof of source truth.

These controls should be proportionate to the pilot. Do not require a hosted identity system or enterprise security programme before a useful local demonstration. Hosted/multi-user expansion needs its own concrete access-control acceptance.

## 17. Monitoring integration

Keep orchestration outside the renderer/evaluator. Existing n8n or agent scheduling can call an assessment/evaluation operation and deliver notifications. Do not add an autonomous scheduler to the core merely because a diagram has a feedback arrow.

A monitor definition includes case/framework revision policy, sources, input mappings, schedule/event mechanism, freshness requirement, assessment contract, notification route, deduplication key and failure behaviour. Case-policy changes require explicit adoption rather than a running monitor silently following any mutable template.

Separate observation events, evaluation events and notification events. Persist the event identity and outcome so a retry does not send duplicate alerts. A failed retrieval is not “no change.” Soft-signal hysteresis records its rule and cannot suppress known hard-condition matches.

## 18. Export, migration and replay

Working exports should contain sufficient schema/framework/input/assessment identity to reproduce the evaluation, with sensitive-data warnings. Static exports should carry the exact snapshot and show that they are not live. Sanitised template exports remove client values, identity, private evidence and capability URLs while retaining tested structure and education.

Preserve unknown and unresolved states in all representations. A screenshot alone is not a complete working record. Export displayed what-if values only when the export is explicitly a scenario/snapshot of those values; do not label them as saved observations.

Schema migrations should be versioned, validated and reversible via backup/history. Never silently change operators, units, lifecycle or policy to make an old case load. Preview consequential migration differences. Historical replay may require a retained compatible evaluator; when unavailable, state that exact replay is unavailable rather than claim equivalence.

## 19. Performance and operational targets

Provisional target workload for the first reusable engine: up to 100 semantic nodes, 200 relationships and 200 evidence references per case, with only concise excerpts loaded in the initial view. This is an engineering test envelope, not a claim about current performance or a product maximum.

Aim for local deterministic recomputation at p95 below 100 ms on a named reference desktop for that fixture, excluding model calls, file/network retrieval and rendering. Record cold/warm timings separately. Prefer a responsive first interaction and stable layout over aggressive animation.

Use lazy evidence expansion and cache deterministic results safely. Measure model request counts, payload size, latency and known cost separately. Provider unavailability must not freeze the interface.

Document startup, shutdown, recovery, runtime requirements and a one-command test path once implemented. The older pilot declared Node 22+, while Archify declares Node >=18; reconcile actual code requirements instead of copying both inconsistently.

## 20. Implementation freedom and extension rule

The IDE lead can choose the simplest arrangement that meets the current slice, replace a weak proposed field name, reuse compatible existing code, add justified dependencies and reorganise files. Material semantic changes should be discussed or recorded according to their impact, not blocked by the existence of this document.

Before promoting a new module/template, require a declared input/output contract, assumptions, supported instrument/lifecycle scope, examples, edge-case tests and user-facing explanation. This is a repeatable development checklist, not a demand for complete formal verification or all future capabilities before shipping the current slice.

Sources and review limits are recorded in the [product specification](PRODUCT-SPEC.md#20-source-basis-and-review-limits). No executable API or runtime implementation is introduced by this documentation commit.