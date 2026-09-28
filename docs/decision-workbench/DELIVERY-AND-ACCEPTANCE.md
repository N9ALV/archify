# IQ Decision Workbench — delivery and acceptance

**Status:** adaptable delivery map, 28 September 2026. The IDE lead owns implementation sequencing with Adam. Read [Product specification](PRODUCT-SPEC.md), [Technical specification](TECHNICAL-SPEC.md), and [IDE handover](IDE-HANDOVER.md).

This plan distinguishes the first useful product from the broader vision. It is not a waterfall approval process: the IDE agent can complete a coherent assigned increment, fix issues and move through its dependent tasks without requesting permission at every heading. Later-stage tests are not blockers for an earlier explicitly scoped pilot.

## 1. Review findings and initial engineering backlog

| ID | Finding from reviewed material | Recommended response | Scope |
|---|---|---|---|
| B01 | Archify interaction prototype hard-codes nodes, values and evaluation in HTML/JS | Introduce one semantic input contract driving both controls and evaluation | First vertical slice |
| B02 | Empty numeric inputs are coerced through `Number`, so blank can become zero | Preserve missing separately; add blank/zero/false tests | First vertical slice |
| B03 | Thesis defaults true and has no unknown control in the prototype | Start real cases unresolved and provide explicit unknown state | First vertical slice |
| B04 | JSON routes and HTML evaluation/display do not have identical trace semantics | Use one evaluator and explicit decisive/visited/informational trace states | First vertical slice |
| B05 | Numeric comparison truth can be mistaken for a favourable result | Separate matched condition, role, severity/effect and final outcome | First vertical slice |
| B06 | “Thesis drift” points are illustrated without a measurement rubric | Keep synthetic or replace with well-defined conditions; do not feed raw AI confidence into it | Template review |
| B07 | Prototype lacks the proposed provenance, freshness, revision and conflict contracts | Add minimal complete records and persistence; reuse verified earlier code if available | Reusable pilot |
| B08 | Earlier separate pilot reports meaningful engine/store/UI tests, but its package was not inspected here | Locate and assess an authorised existing copy; port compatible logic/tests rather than restart unnecessarily | Bounded initial review |
| B09 | Earlier pilot did not accept native browser navigation/module loading/Windows/IQ Browser end to end | Run actual native acceptance on the intended platform; label container/harness evidence accurately | Platform acceptance |
| B10 | Upstream diagram skill has artefact freeze and layout instructions for static deliveries | Scope them correctly; do not let them freeze product code or force an unreadable workbench | Handover/architecture |
| B11 | Live TypeSafe documentation did not load in this review | Verify SDK/API at implementation; develop against a mock adapter in parallel | Optional AI lane |
| B12 | Fork is public and Issues are disabled at review | Keep documentation here; keep client data/private packages out; do not change repo settings automatically | All increments |

These are source-review findings, not a claim that this handover ran the application or exhausted every possible defect.

## 2. Milestone map

### M0 — orient, reuse and choose the first implementation seam

**Goal:** avoid duplication and architectural dead ends without turning discovery into another long planning project.

Inspect current branch/local state, current product docs and any authorised existing 0.1.0 pilot. Establish what actually exists, what works and what is merely documented. Choose whether the first generic workbench uses a dedicated HTML renderer with an Archify adapter, or a clean new renderer/type in the fork. Record a short decision explaining reuse and rejected alternatives.

**Concrete output:** inventory, working baseline, chosen seam, initial runnable fixture and a short next-slice plan. Preserve the old prototype/examples as historical references unless clearly redundant.

**Do not block on:** obtaining a private package that is not readily available, a new brand name, Jev credentials, cloud architecture, Issues being disabled, or a decision about every future node type. State the missing reuse opportunity and continue with accessible code.

### M1 — one complete, generic, manual-input workbench

**Goal:** prove that the same semantic record drives visible controls, rule evaluation and saved/reopened state.

Use the opportunity-assessment flow as the first slice. Provide a compatible template and one labelled synthetic case. Implement missing/false/zero handling, numeric comparisons, explicit outcome meanings, a useful rule trace, node-owned controls and basic evidence details. Separate scenario changes from saved state. Include a checked save path or an explicit scenario export/agent-apply path and working reopen.

Provide a local browser launch path and a concise runnable developer guide. Show a baseline, failed condition and unresolved-input case. Do not let a UI-only mock stand in for the evaluator/store contract.

**Acceptance:** relevant core tests pass; the real app is usable in a normal supported browser on the tested development platform; save/reopen and scenario distinction are demonstrated. Report any Windows/IQ Browser checks still outstanding rather than pretending they passed.

**Deliberately absent:** live Jev, autonomous monitoring, hosting, advanced simulation and order execution.

### M2 — reusable client pilot and education

**Goal:** demonstrate that this is a reusable decision product rather than one attractive example.

Add portfolio-addition, existing-position review and scenario-expectancy templates using the same runtime. Reuse verified compatible earlier pilot code/tests. Implement provenance/freshness, conflict-safe writes/history, basic baseline/scenario comparison, evidence expansion, educational disclosure and meaningful diagnostics. Support supported import/export formats and a clean actual-size view.

Complete native Windows/IQ Browser acceptance when the environment is available. The application should remain usable in the system default browser when IQ Browser is unavailable. Avoid requiring clients to install development/test dependencies.

**Acceptance:** four template journeys, lifecycle/precedence tests, arithmetic and unit tests, actual persistence/conflict recovery, representative desktop layouts and a short comprehension walkthrough with Adam. An installed-client test is a release criterion for that client platform, not a reason to suspend unrelated development.

### M3 — main-agent authoring and one bounded semantic assessment

**Goal:** prove useful AI assistance without coupling the engine to a provider.

Expose actual capability/contract discovery and typed create/read/update/evaluate/scenario operations. The assistant should make/update a case without rewriting renderer code. Give it contextual educational/research actions and a truthful route to read unsaved browser state or use scenario exports.

Add one semantic question, preferably a comparison of two supplied announcements/passages with outcomes changed / explicitly unchanged / not addressed / cannot determine. Implement a mock adapter, then the actual configured provider when credentials/docs are available. Bind responses to evidence versions, record outcomes, handle failure and stale responses, and collect labelled examples for evaluation.

**Acceptance:** authoring journey works; deterministic core remains available offline; malformed/uncertain/stale responses do not become facts; mock versus live evidence is clearly labelled; the narrow model feature has a documented evaluation result before broader claims.

**Do not block on:** a missing Jev key. Finish adapter, fixtures, manual fallback and user experience; report live validation as the only outstanding integration check.

### M4 — sensitivity, comparison and decision review

**Goal:** expose what would change the result and preserve reasoning over time.

Extend baseline/scenario differences, numeric boundary inspection and evidence/assumption/policy change attribution. Add decision-history review and initial linked-case/shared-capital warnings. Compare compatible alternatives without manufacturing rankings across incompatible horizons or currencies.

Retain original and revised evaluations so outcome hindsight does not rewrite the initial case. Add presenter/teaching refinements based on actual use, not a separate rendering engine.

**Acceptance:** users can identify what changed, which change was decisive and which conclusions remain unsupported; historical state can be inspected without fresh model calls masquerading as replay.

### M5 — optional monitoring and distribution

**Goal:** reuse the workbench framework in explicitly configured recurring observation workflows.

Use existing orchestration where suitable. Implement source mapping, freshness, idempotent observation/evaluation/notification events, duplicate suppression, bounded semantic checks and visible retrieval failure. Keep monitor adoption of framework/policy changes explicit. Test public/private export and existing distribution entitlement as applicable.

**Acceptance:** actual end-to-end observation-to-review event on synthetic or authorised data, duplicate/retry behaviour, visible service failure, no unintended external actions, and accurate status in the workbench. Production publication/hosting is a separate explicit deployment scope.

### M6 — selected advanced modules

Choose based on user value demonstrated in prior milestones: risk sizing, richer stress tests, simulations, Bayesian updates, portfolio interaction or multi-criteria preferences. Each module needs a declared domain, assumptions, data requirements, deterministic contract, educational layer and tests. There is no requirement to build all of them.

## 3. Requirements-to-evidence map

| Requirement | Product section | Technical section | Main acceptance IDs |
|---|---|---|---|
| R01 Frame the actual decision and lifecycle | 7–8, 11 | 4, 8 | F01–F04, L01–L05 |
| R02 One specification drives behaviour and display | 2, 6 | 1, 5–7, 14 | G01–G06, U01 |
| R03 Preserve uncertainty and provenance | 7, 10 | 4, 6, 10 | V01–V06, E01–E05 |
| R04 Correct comparisons and scenario arithmetic | 11, 14 | 9 | N01–N08 |
| R05 Keep saved and what-if state distinct | 8–9 | 11–12 | S01–S08 |
| R06 Explain results and teach in context | 9–12 | 4.7, 14–15 | U02–U08, C01–C04 |
| R07 Bounded optional AI, functioning offline core | 13 | 12–13 | A01–A10 |
| R08 Lifecycle-specific precedence | 11.3 | 8 | L01–L05 |
| R09 Portable, private and recoverable records | 18 | 11, 16, 18 | P01–P08 |
| R10 Reusable later monitoring/replay | 15–16 | 17–18 | M01–M06 |
| R11 Low-friction agent and client operation | 4, 8, 19 | 12, 19 | O01–O06 |

References name sections, not immutable implementation filenames. Refine this matrix as the design changes.

## 4. Acceptance fixtures and expected behaviour

Use synthetic data for reproducible tests. Automated tests, visual inspection, model evaluation and user comprehension are different evidence categories; none substitutes for the others.

### 4.1 Framing and compatibility

| ID | Fixture/action | Expected result |
|---|---|---|
| F01 | Create a real case from a populated demo | Material facts/policies do not carry over silently; synthetic example remains separately labelled |
| F02 | Open pre-entry versus live-position case with identical numeric values | Correct lifecycle-specific outcomes and labels |
| F03 | Apply long-only position template to unsupported short/option case | Clear incompatibility, not an approximate result presented as valid |
| F04 | Provide conflicting horizon/currency/portfolio scope | Visible unresolved frame or incompatible calculation; no guessed conversion |

### 4.2 Graph and single-source behaviour

| ID | Fixture/action | Expected result |
|---|---|---|
| G01 | Change a permitted threshold in a semantic test fixture | Control, comparison, route and explanation all use the same new value |
| G02 | Duplicate node ID or missing output target | Exact validation diagnostic; no silent node merging |
| G03 | Executable cycle | Rejected/bounded according to supported contract; no recursive loop |
| G04 | Review relationship loops to research | Can be displayed without executing a recursive evaluation |
| G05 | Branch skips a downstream criterion | It is marked skipped/not decisive, not passing |
| G06 | Unsupported operator/group/module | Explicit unsupported diagnostic, not coerced behaviour |

### 4.3 Values, missingness and logical state

| ID | Fixture/action | Expected result |
|---|---|---|
| V01 | Clear expected return or exposure field | Missing/unknown, never numeric zero |
| V02 | Enter actual numeric zero | Zero retained and evaluated normally within the module domain |
| V03 | Set Boolean false versus unknown | Different states and correct branch behaviour |
| V04 | Enter non-finite/invalid numeric value | Rejected or error state; no favourable result |
| V05 | Known failed hard entry criterion plus missing unrelated input | Failed criterion remains visible along with incomplete coverage |
| V06 | Supported all/any group combinations with unknowns | Declared truth table, with independent errors/eligibility preserved |

### 4.4 Arithmetic and domain basis

| ID | Fixture/action | Expected result |
|---|---|---|
| N01 | Expected 14%, required 10%; exposure 6%, max 8%; thesis true | Configured entry criteria satisfied, not execution/approval |
| N02 | Expected equals 10% | `>` fails; `>=` matches; UI and receipt agree |
| N03 | Gross scenario returns −20%, +8%, +30%, probabilities 25/50/25% | Expected gross 6.5%; after common cost of 1 percentage point applied once, net 5.5% |
| N04 | Probabilities total 90%, include a negative or omit an outcome probability | Invalid/unresolved distribution; no silent normalisation |
| N05 | Cost already included in net outcomes | Cost is not subtracted again |
| N06 | 100,000 portfolio, sector 24,000, buy 8,000 | From existing cash: 32%; external capital addition: about 29.63%; funding source explicit |
| N07 | Mixed currencies, horizons or gross/net bases | Comparison refuses unsupported equivalence and identifies mismatched fields |
| N08 | Value differs at hidden precision near a threshold | Calculation uses declared precision, not rounded display value |

### 4.5 Lifecycle and precedence

| ID | Fixture/action | Expected result |
|---|---|---|
| L01 | Live case: known hard trigger and favourable soft assessment | Hard-trigger result retained; soft score cannot override it |
| L02 | Live case: unknown required hard condition, no known trigger | No reassuring “no configured trigger detected” claim |
| L03 | Live case: known hard trigger plus missing soft input | Trigger reported with incomplete secondary evidence, not suppressed |
| L04 | New-entry hurdle fails on an already owned position | No automatic lifecycle change, close instruction or recorded fill |
| L05 | Closed case opened with newly available data | Historical record preserved; new evaluation explicitly separate |

### 4.6 Evidence and freshness

| ID | Fixture/action | Expected result |
|---|---|---|
| E01 | Reopen old data today | Saved/retrieved/evidence-as-of/evaluation dates remain distinct |
| E02 | Relevant input expires under freshness policy | Affected current assessment becomes stale/ineligible; historical source preserved |
| E03 | Two material sources contradict | Both retained with unresolved state or recorded resolution |
| E04 | Model assessment based on old evidence returns after an edit | Not silently applied to the new snapshot |
| E05 | Source link exists but no point-in-time content snapshot | Receipt states reproduction limitation rather than claiming immutable evidence |

### 4.7 Scenarios, saves and recovery

| ID | Fixture/action | Expected result |
|---|---|---|
| S01 | Edit browser scenario | Saved record remains unchanged; scenario label and overrides visible |
| S02 | Disk case changes while scenario is dirty | Dirty work preserved and conflict notice shown |
| S03 | Apply scenario against stale base hash | Rejected with inspect/reconcile path; no blind overwrite |
| S04 | Two writers update the same revision concurrently | Only compatible/serialised update succeeds; no lost update |
| S05 | Interrupt a save | Recover complete old/new revision; no partial JSON presented as valid |
| S06 | Corrupt current file | Visible diagnostic and recoverable history; no silent default/demo replacement |
| S07 | Restore historical revision | New recorded revision or explicit restoration receipt; history retained |
| S08 | Scenario proposes policy/lifecycle change | Differentiated from routine observation update and handled under actual user authority |

### 4.8 Optional assessment provider

| ID | Fixture/action | Expected result |
|---|---|---|
| A01 | No provider key/network | Manual/deterministic core works; optional assessment unavailable |
| A02 | Wrong choice key, omitted required answer or invalid probability | Invalid response retained as diagnostic, never silently consumed |
| A03 | Valid insufficient-evidence/no-match answer | Unresolved input and useful next-work explanation |
| A04 | Change question meaning/version or source content | Previous cached assessment is not reused as equivalent |
| A05 | Independent questions batched | Correct independent state; dependent questions use a later stage when needed |
| A06 | Slider changes deterministic operand only | Local calculation, no unnecessary provider call |
| A07 | Retrieved text contains instructions to change policy | Remains evidence text; no policy/tool-authority escalation |
| A08 | Model confidence is high | Still labelled an assessment; not investment probability or permission |
| A09 | Mock returns expected values | Receipt says mock; no claimed model-quality result |
| A10 | Representative live labelled set with no-match/negation/scope changes | Document measured error/abstention profile and limitations; do not assume a universal threshold |

### 4.9 User interface and understanding

| ID | Fixture/action | Expected result |
|---|---|---|
| U01 | Change node input | Accurate result/path from shared evaluator, without wholesale layout churn |
| U02 | Expand evidence and a long explanation | Nodes reflow, connectors avoid unrelated nodes, controls remain reachable |
| U03 | Keyboard-only traversal | Visible focus, labelled controls, usable editing/inspection and return path |
| U04 | Dark/light and reduced motion | Meaning retained without colour or motion dependence |
| U05 | 1440×900, 1920×1080, 2560×1440 plus a narrower window | Readable actual-size canvas, usable containment and no escaped controls |
| U06 | Outcome is a matched adverse condition | Text/styling communicate adverse effect, not generic green PASS |
| U07 | Open education | Relevant definition/example without changing saved assumptions |
| U08 | Inspect a static export | Snapshot date, scope, unresolved states and synthetic status remain visible |
| C01 | User asked why the current result occurred | Identifies decisive condition without a developer explaining the graph |
| C02 | User asked which fact is missing and what to research next | Identifies a material missing input and appropriate next work |
| C03 | User asked whether scenario edit changed the saved case | Correctly distinguishes hypothetical and saved state |
| C04 | User sees a losing realised outcome after a reasonable process | Review view does not automatically declare the original decision irrational |

### 4.10 Privacy, operational and monitoring tests

| ID | Fixture/action | Expected result |
|---|---|---|
| P01 | Traversal/symlink/out-of-scope file request | Rejected by the chosen local-file boundary |
| P02 | Unexpected origin/Host or missing required local capability | Rejected according to server contract |
| P03 | Evidence contains HTML/script | Rendered safely as data; no code execution |
| P04 | Export sanitised template | No client values, private evidence, keys or capability URLs |
| P05 | Unsupported schema migration | Diagnostic and preserved original; no silent semantic rewrite |
| P06 | Working-record versus scenario export | Correctly labelled values and revisions; no false saved-state claim |
| P07 | Provider logging | No credentials or unnecessary client content in logs/fixtures |
| P08 | Real private distribution check, when that lane ships | Entitled access works and non-entitled access is not accidentally opened |
| O01 | Normal supported-browser launch | Native navigation and modules actually load; no injected-harness equivalence claim |
| O02 | Windows/IQ Browser startup/reopen/shutdown | Actual installed-client evidence for those claims; fallback browser works |
| O03 | Agent authors a case and updates evidence | Uses semantic operations, not regenerated HTML |
| O04 | Agent has only disk state, browser has unsaved edits | Does not claim to know unsaved values; uses actual bridge/export |
| O05 | Routine reversible task is already authorised | Completes without redundant approval prompts |
| O06 | Provisional performance fixture | Records device/runtime and p50/p95, separating evaluator, render and provider timings |
| M01 | Same source event retried | One observation/evaluation identity and no duplicate notification |
| M02 | Source retrieval fails | Visible service failure, not “nothing changed” |
| M03 | Hard-condition event amid soft-signal hysteresis | Hard event not silently delayed/suppressed |
| M04 | Framework changes while watcher is active | Adoption is explicit/versioned; old monitor semantics do not silently drift |
| M05 | Historical replay | Uses recorded inputs/assessment/evaluation clock; no fresh model call presented as replay |
| M06 | Browser file polling only | Never labelled a live market-data watcher |

## 5. Representative demonstration script

Use the same running application and saved test records, not a set of disconnected mock screens.

1. Open a synthetic opportunity case. Explain question, horizon, existing/new distinction and the separate origins of observations and policies.
2. Clear one numeric input. Show unknown and why a result cannot be completed. Re-enter zero to demonstrate that zero is a real value.
3. Restore the baseline, change a return assumption across an equality boundary and show the exact operator's effect.
4. Change the exposure assumption in a what-if scenario, compare it with the saved baseline and revert without touching the saved case.
5. Expand evidence/education and demonstrate layout reflow and an understandable explanation.
6. Save an authorised change, reopen it and show the actual revision. Trigger a concurrent-update conflict and recover without losing either version.
7. Open a live-position case. Demonstrate a hard trigger, an unknown required hard input and an ordinary softer review change.
8. Open scenario expectancy. Show the 6.5% gross / 5.5% net example, then invalidate the probability total and show the unresolved calculation.
9. When the AI lane exists, demonstrate a model assessment, abstention and provider failure without breaking manual operation. Label mock versus live runs.

The first M1 demonstration uses only the subset implemented in that slice; do not pretend later steps exist.

## 6. Test strategy without overtesting paralysis

Run targeted unit/contract tests while implementing, then the relevant integration/browser checks for the changed surface. Run broader regression at meaningful integration points and before labelling a release. Do not repeatedly rerun unchanged expensive suites after every prose or cosmetic edit.

When a test fails, investigate the actual failure, fix it and rerun the affected checks. Repeated unchanged attempts should cause a change of tactic, a smaller reproduction or a documented limitation—not an indefinite loop or a request for Adam to approve routine debugging.

A blocked platform test should be reported precisely. Continue other work; do not claim a native pass from an injected harness. A known correctness/privacy defect affecting real use blocks claiming that affected capability ready, but does not prohibit delivering a clearly marked development demonstration or completing independent modules.

Test semantics and interface reality separately. A validated JSON shape does not establish sound investment logic; a screenshot does not establish save correctness; a correct arithmetic fixture does not establish model calibration.

## 7. Delivery evidence per increment

Each meaningful implementation handoff should contain:

- Commit/branch and the implemented scope, with the current documentation updated where it changed.
- Actual launch/test commands generated from the implemented project, with no placeholder setup.
- A runnable case/demo and a brief statement of how to use the changed features.
- Automated test results, actual browser/platform evidence and a clear distinction between inspected, tested, mocked and untested.
- Known limitations and one recommended next slice. Separate genuine blockers from non-blocking improvements.

Do not claim shipping, publication, entitlement, live model performance or installed-client acceptance without the corresponding evidence. Preserve a recoverable checkpoint before material restructuring; avoid a destructive reset of unrelated or concurrent work.

## 8. Decisions that remain open

| Decision | Working default | When it needs resolution |
|---|---|---|
| New Archify diagram type versus dedicated workbench renderer/adapter | Clean, isolated module; reuse Archify where it genuinely helps | M0 implementation seam; IDE may choose with rationale |
| Reuse of earlier 0.1.0 code | Inspect an authorised copy and reuse compatible engine/store/tests | Early, but absence is not a blocker |
| Runtime and dependency policy | Small maintainable local JS/TS stack; reconcile actual Node requirements | First runnable slice |
| Client save UX | Separate what-if state; checked agent apply is acceptable initially | M1/M2 usability review |
| Semantic provider and thresholds | Provider-neutral adapter; no required live provider for core | M3 live integration |
| Initial template wording/policies | Synthetic examples and unknown real defaults | Iterative review with Adam |
| Hosted/embedded deployment | Preserve contracts; do not build new hosting/identity by default | After local value is demonstrated or Adam redirects |
| Monitoring integration | Existing orchestration, separate from renderer | M5 or earlier explicit priority |
| Advanced modules | Select one demonstrated need, not all possible concepts | After core comprehension/usefulness review |
| Public/client release scope | Honest pilot labelling; practical domain/distribution review before expanded offering | Before the relevant actual release, not before coding |

No unresolved row here is an instruction to stop all work. The IDE lead should select sensible reversible defaults and raise only the decision that materially affects the assigned slice.

## 9. Current status at this documentation handover

This handover adds a detailed design and delivery plan. It does not implement the proposed engine, modify the existing runtime, run the earlier pilot's tests, activate Jev, deploy a server, schedule a watcher or publish a client package. The source-review findings and prior reported tests are distinguished from future acceptance above.

The next lead should update this status with actual evidence as work progresses. This plan is intended to accelerate that work, not bind it to the original author's preferred implementation.