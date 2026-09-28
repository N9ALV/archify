# IQ Decision Workbench — product specification

**Status:** living product baseline and engineering handover, not a frozen contract.  
**Prepared:** 28 September 2026.  
**Repository baseline reviewed:** `307fc4b353e75eb23d620c727891515955fa3aa3`.  
**Product owner:** Adam. **Next implementation/design lead:** the IDE agent working with Adam.  
**Working name:** IQ Decision Workbench; naming and packaging remain open.

Read this with [Technical specification](TECHNICAL-SPEC.md), [Delivery and acceptance](DELIVERY-AND-ACCEPTANCE.md), and [IDE handover](IDE-HANDOVER.md). The handover explicitly grants ordinary implementation discretion. Detailed requirements here describe the intended product, not a requirement to build the entire roadmap before delivering something usable.

## 1. The product in one paragraph

A browser-first, persistent, AI-assisted decision workbench that makes an investor's or trader's reasoning visible and usable. The user and their AI assistant establish a question, alternatives, evidence, assumptions, constraints and review conditions. A reusable interface presents these as interactive nodes in an intelligible decision map. A deterministic engine evaluates the declared rules. Users can change assumptions in a clearly marked what-if scenario, inspect why a route changed, discover which information matters, and retain the original reasoning for later review. An optional typed semantic model such as Jev can assess narrowly defined questions about supplied evidence; a general-purpose agent handles research, explanation and framework construction. Neither the picture nor an AI confidence value is a guarantee about an investment.

The central promise is **better visibility into the decision and its dependencies**, not a prediction service or an automatic buy/sell machine.

## 2. Why this is more than a diagram

The motivating problem is not lack of charts. Many non-professional investors have fragments of an argument, an attractive return estimate, a price chart and a feeling about risk, but no explicit connection between them. Even sophisticated concepts are of limited practical use when presented as isolated definitions or opaque scores.

The workbench connects six activities in one durable object:

1. **Frame:** what decision is actually being made, over what horizon, against what alternatives?
2. **Understand:** what do the relevant concepts mean in this particular case?
3. **Substantiate:** which statements are observations, estimates, assumptions or policies, and what supports them?
4. **Evaluate:** what follows from the declared relationships and rules?
5. **Explore:** which plausible changes alter that result, and what remains unknown?
6. **Review:** what changed after the original assessment, and was the reasoning sound given what was known then?

The graph is simultaneously a working interface, an explanation of dependencies and a record of the framework. It is not decoration added after an AI has already produced a verdict. The same underlying specification should drive the graph, calculations, status explanations and any later monitoring evaluation.

Do not claim this category is unprecedented or validate demand through novelty alone. Treat adoption, comprehension and usefulness as hypotheses to test with Adam and representative users.

## 3. Outcomes the product should help users achieve

A user should be able to answer, in ordinary language:

- What is the actual question, and am I evaluating a new entry, an addition, an existing position or a retrospective review?
- What must be true for the proposed course to make sense under my stated framework?
- What is known, assumed, disputed, stale or missing?
- Which constraints are hard limits and which are preferences or prompts for review?
- What would change the framework's result, and which of those changes are plausible?
- What remains to research or decide, rather than simply fill into a form?
- Why is this framework appropriate for this instrument, horizon and purpose?
- How would this affect the rest of my portfolio or compete for the same capital?
- What was the original reasoning, and what changed since then?

Success is not more trades, more alerts, more green nodes or more time spent in the application. A useful outcome may be to wait, reject the idea, reduce the scope of the question, collect evidence, or recognise that the framework is not suitable.

## 4. Audience and operating roles

### 4.1 Guided private investor

May have meaningful capital and practical experience but little desire to manipulate spreadsheets, write rules or learn a graph editor. Needs accessible wording, explicit assumptions, a manageable first screen and assistance at the point of confusion. Must not have to understand JSON, Jev, dependency graphs or model routing.

### 4.2 Active trader or systematic investor

Needs a repeatable process, clear entry versus management logic, units, costs, scenario distributions, risk budgets and dated evidence. May want more detail, but the product must not assume that all strategies reduce to the same indicators or thresholds.

### 4.3 Educator or presenter

Uses synthetic examples and controlled what-if changes to show how a decision works. Needs a clean presentation view and a way to distinguish demonstration assumptions from client-specific records. The underlying rules must not change between teaching and normal views.

### 4.4 IQ Wealth or another authorised assistant

Constructs and updates semantic records, helps source information, explains concepts, selects appropriate templates and proposes revisions. Uses a documented application contract rather than rewriting HTML for each case. Can work proactively within the user's task and established permissions; routine research and non-destructive updates should not require repetitive approval.

### 4.5 Product developer / template maintainer

Owns implementation, reusable contracts, tests and template quality. This role is distinct from the client-side assistant operating a workbench. The IDE agent leads this work after handover and may improve this specification with Adam.

## 5. Positioning and boundaries

The product is a decision-support workpaper with interactive explanations. It is not, by default:

- a stock recommender, investment-quality rating or promise of profitable performance;
- a universal optimiser, backtester, broker terminal or order-execution system;
- a general-purpose visual automation platform replacing n8n;
- a requirement to expose every professional concept on the first screen;
- an AI-generated application rebuilt from scratch for every user request.

These are current scope boundaries, not a prohibition on future development. Any later execution, hosted sharing or regulated client-facing offering needs a deliberate product/integration decision; their absence does not prevent a local decision-support pilot.

## 6. Product principles and working defaults

### 6.1 Truthful semantics

Missing is not zero or No. Observations are not policies. AI assessments are not observations merely because they have a numeric confidence. A matched condition is not necessarily favourable. A passed set of configured rules is not an approval, a fill or proof of suitability.

### 6.2 Progressive disclosure

Begin with the question, a short main path, the current result and the most consequential unresolved issues. Reveal evidence, methodology and detailed dependencies on demand. The initial overview should usually have roughly five to nine primary groups, not dozens of indistinguishable cards; this is a design target, not a hard technical limit.

### 6.3 Stable interface, editable meaning

The renderer owns layout, control behaviour and connection routing. The agent supplies domain values, relationships, labels and sources. Users should not have to rearrange boxes to make the product usable.

### 6.4 A useful non-AI core

Manual inputs, deterministic evaluation, scenarios, evidence inspection and saved records remain functional without a semantic provider or general-purpose model connection. Unavailable AI is a visible capability state, not a reason to disable the application.

### 6.5 Local browser first

Start with a local browser workbench, preferably opened through IQ Browser when available, otherwise the system's modern default browser. Do not use IQ Viewer as the default surface. Preserve the possibility of embedding the same UI later without requiring an iframe or building a second evaluator.

### 6.6 Separate exploration from commitment

Browser edits are scenario state until deliberately saved or applied through an already authorised workflow. A scheduled observation, a rule evaluation, a notification and an external transaction are separate operations.

### 6.7 Comprehension over spectacle

Motion, colours and diagram geometry must not imply relationships, certainty or activity that the data does not establish. Use text labels and accessible controls, not colour alone. Do not animate routine calculations as though the system were performing sophisticated reasoning.

## 7. Conceptual model and terminology

| Term | Meaning in this product |
|---|---|
| Framework / template | A reusable, versioned structure of questions, inputs, relationships and rule semantics. |
| Case | One application of a framework to a specific decision, instrument, portfolio question or learning example. |
| Policy | A chosen constraint or operating rule, such as a maximum exposure. It is not inferred from today's data. |
| Observation | A dated, sourced measurement or statement about the world. Source inclusion does not itself verify correctness. |
| Estimate | A calculated or judgement-based value with a method and assumptions. |
| Assumption | Something provisionally taken as true for a stated purpose, including scenario inputs. |
| Assessment | A human or model interpretation of evidence, identified as such. |
| Evidence item | The source reference and relevant content, with dates, scope and an integrity reference when available. |
| Node | A displayed information, question, calculation, condition, group or outcome element. |
| Evaluation | A deterministic result for a particular validated framework, input snapshot and evaluation time. |
| Scenario | A named set of hypothetical differences from a saved case revision. |
| Decision record | The framework, inputs, reasoning, evaluation and user disposition retained for review. |
| Watcher | A separately configured process that obtains observations and invokes evaluation; not browser file polling. |
| User disposition | What the user chose to do, which may differ from the framework's result and is recorded separately. |

Risk must specify what it means: likelihood, magnitude of loss, volatility, drawdown, exposure, liquidity, uncertainty or another explicitly defined dimension. Avoid using a single label to hide different concepts.

## 8. Primary end-to-end journey

### 8.1 Start with a real question

Illustrative request: “Help me assess whether adding this position fits the way I am investing.”

The assistant checks available context and asks only for information that materially changes the framework: objective, instrument, horizon, existing/new position, relevant portfolio scope, alternatives and known constraints. It should use facts already supplied rather than run a repetitive onboarding questionnaire.

It proposes an appropriate template and explains why. For a simple factual question, it answers normally instead of forcing the user into a workbench.

### 8.2 Establish the decision frame

The opening summary names the question, lifecycle, horizon, valuation/return basis, portfolio scope and meaningful alternatives, including waiting or doing nothing. Unsupported instruments or missing context stay visible. A long-only share template must not silently masquerade as an options or short-selling model.

New real cases start with unknown material inputs. Demonstration cases may be populated, but are conspicuously labelled synthetic and do not silently become user policies.

### 8.3 Build and explain the framework

The assistant creates semantic data using a checked template. The interface shows the main path and the questions attached to each stage. The user can ask why a node is included, remove an inappropriate assumption through a framework revision, or ask for more detailed analysis.

The product should be capable of saying “this template is not a good fit” rather than manufacturing a result.

### 8.4 Populate evidence and assumptions

Inputs may come from the user, approved data connectors, calculations, saved research or a bounded semantic assessment. Every material input retains origin, relevant date, scope and method. Conflicting sources remain distinguishable instead of one silently overwriting the other.

The user can see what is missing without being forced to invent a number. The assistant can work on answerable research while other fields remain unresolved.

### 8.5 Inspect the current evaluation

The outcome panel states what the configured framework currently establishes, its decisive reasons and important unresolved conditions. It distinguishes “criterion not met” from “not enough information,” “comparison invalid” and “not applicable.”

The map highlights the applied route and other relevant conditions. A known hard condition is not hidden by an unrelated favourable score or a missing soft input.

### 8.6 Explore alternatives and sensitivity

The user changes assumptions within relevant nodes. The original saved case stays intact. The interface identifies changes, recalculates locally, and explains which changes actually affected the result.

The user can compare saved baseline, active scenario and another named scenario. Comparisons retain equal horizons and return bases or explicitly report incompatibility. The application must not manufacture a ranking when cases are not comparable.

### 8.7 Record the disposition

The user can retain the case, save selected changes, record a decision to wait, request further research or archive the idea. A user disposition is not a broker event. Marking a case as live requires actual position context, not an evaluation that says the entry rules passed.

### 8.8 Return and review

On reopen, the workbench shows what is saved, what is stale and what changed. New evidence can be compared to the earlier snapshot. The user can see whether a changed result came from new observations, changed assumptions, changed policy, a framework revision or a different model assessment.

## 9. Core product surfaces

### 9.1 Case launcher

Recent cases, create from template, open an existing record, import a supported record and open a labelled demonstration. Show case title, lifecycle, last saved/reviewed dates and unresolved status; avoid a dashboard full of unexplained scores.

### 9.2 Case header

Question, instrument or portfolio scope, horizon, lifecycle, saved revision, data freshness summary and current scenario mode. Distinguish “saved at,” “evaluated at” and “evidence as of.” A recently opened old record is not fresh research.

### 9.3 Interactive canvas

Controls live inside the nodes that own the criteria. Node height responds to content; connections are measured/routed around actual bounds. Maintain readable text at actual size with contained canvas navigation rather than shrinking the entire graph to illegibility.

Provide fit-to-view, readable/actual-size view, keyboard navigation, focus on the active path and a way to return to the full framework. Support narrow windows through contained scrolling or a linear representation of the same nodes. Do not change semantics when changing layout.

### 9.4 Node detail / evidence inspector

One focused inspector rather than many permanent panels. Show the question, value, unit, evidence, origin, method, dates, current status, relevant rule and dependencies. Include “Explain,” “Find evidence,” “Challenge this assumption” and “Compare alternatives” actions where supported. These actions send the selected node and relevant case context, not an unbounded dump of every client file.

### 9.5 Outcome and next-work panel

Show a plain-language rule result, reasons, unresolved issues and relevant next work. Example: “The return comparison is satisfied, but the portfolio constraint is not. The estimate is also due for review.” Do not compress these into an unqualified “Buy.”

Next-work suggestions should connect to actual missing or sensitive inputs. Routine details can be completed automatically within an existing task; the panel is not a machine for repeatedly asking permission.

### 9.6 Scenario / comparison surface

Clearly label hypothetical inputs, show a change list and permit reset, save as scenario, export and apply selected changes. Explain why some changes cannot be applied automatically, such as a stale base revision or a request to replace a policy with an observation.

### 9.7 Review history

Timeline of saved case changes and evaluations with accessible differences. Preserve the original question and reasoning. Users should be able to distinguish “the outcome was poor” from “the original process ignored a stated constraint.”

## 10. What a node must communicate

A node should answer five questions without requiring developer knowledge:

1. What is being asked or calculated?
2. What input or evidence is currently being used?
3. What is its status and why?
4. Where does it matter in the framework?
5. What can I do here?

Normal compact contents are a plain-language label, value/control, unit, status and a short reason. Expanded contents reveal provenance, methodology and education.

Recommended initial controls are information/evidence, yes/no/unknown, numeric comparison, bounded choice, range and outcome. More complex deterministic calculations can be registered modules rather than arbitrary JavaScript expressions.

An AI-supported node should visibly distinguish a proposed assessment from an accepted input, and preserve that assessment's provider/method and evidence. High model confidence does not erase the distinction.

## 11. Initial template family

These are the intended initial family, not four independent bespoke applications. Implement one complete vertical slice first, then demonstrate the same renderer and evaluator with the others. Reuse the earlier pilot where appropriate.

### 11.1 DEEP opportunity assessment

**Question:** does this new opportunity satisfy the user's stated evaluation framework?

**Flow:** Discover → Educate → Evaluate → Perform planning → Monitor/re-evaluate relationship.

**Typical contents:** question and alternatives; evidence set; thesis and disconfirming conditions; return estimate or linked scenario analysis; required return or other criterion; instrument-specific risk checks; resulting portfolio exposure; remaining implementation considerations.

**Outcomes:** incomplete, further research/review, configured condition not met, or configured entry conditions satisfied. The last means only that the authored conditions are satisfied. An implementation-plan node may organise work but does not submit an order.

**Important distinction:** a broad “thesis intact?” judgement may be recorded by the user/main agent, or supported by narrower evidence questions. Do not automatically convert it to an unrestricted Jev verdict.

### 11.2 Portfolio addition / exposure review

**Question:** what does the proposed addition change about the portfolio, and does it satisfy the declared constraints?

**Typical contents:** current holdings/cash and valuation date; portfolio scope; proposed funding source; resulting concentration; role of the exposure; liquidity needs; supplied stress estimates; overlap/dependence concerns; alternatives.

**Arithmetic example, synthetic:** in a 100,000-unit portfolio with 24,000 units in one sector, buying 8,000 units from existing cash gives 32% sector exposure if prices and total value are otherwise unchanged. Funding the same purchase with 8,000 of new external capital gives 32,000 / 108,000, approximately 29.63%. The denominator and funding source must be explicit.

**Boundary:** ticker count is not proof of diversification. Do not invent a correlation estimate or a “diversification benefit” from a sector label. Multiple candidate cases drawing on the same cash must be flagged as competing uses, not independently approved allocations.

### 11.3 Existing-position review

**Question:** do current observations trigger a stated hard condition, a softer review or continued monitoring under the original management framework?

**Typical contents:** actual lifecycle and position; original thesis; authored hard conditions; relevant current observations; softer review triggers; changed circumstances; alternatives and review notes.

**Precedence:** a known applicable hard-condition match takes precedence over softer favourable assessments. Missing evidence for a required hard condition prevents a reassuring “nothing to review” result. An entry hurdle no longer being satisfied is not automatically an exit instruction.

**Boundary:** a stop-price condition is a trigger, not a guaranteed execution price or maximum possible loss. Instrument-specific semantics are essential; a long-only example is not a valid short/option template.

### 11.4 Scenario / expectancy workbench

**Question:** what follows from an explicit set of possible outcomes, probabilities and costs, and how sensitive is that conclusion to the assumptions?

**Typical contents:** mutually exclusive and collectively exhaustive scenarios as an explicit modelling assumption; return/payoff in compatible units and horizon; probabilities and their basis; cost convention; expected value; downside cases; comparison hurdle; sensitivity.

**Synthetic teaching example:** probabilities 25%, 50%, 25%; gross one-period returns −20%, +8%, +30%. Expected gross return is 6.5%. A 1-percentage-point cost applied once in every scenario gives expected net return 5.5%. These inputs are invented for teaching, not a forecast or recommended policy.

**Boundary:** refuse an expected-value calculation when probabilities are missing or do not sum to 100% within a declared small numerical tolerance. Do not silently normalise or invent them. A positive expected value does not establish attractive tail risk, liquidity, suitability, repeatability or a complete investment case.

## 12. Education as part of the working interface

Education should explain the current decision, not force users through a textbook before they can proceed.

Each template/node should have three disclosure levels:

- **Immediate:** a sentence explaining what the criterion means and why it is present.
- **Worked explanation:** a relevant example, formula or comparison using the case's units, clearly separating synthetic values from saved values.
- **Deeper exploration:** a short lesson, source-backed reference or conversation with the assistant about assumptions and limitations.

Initial learning topics include expectancy versus payoff ratio; likelihood versus severity; exposure versus risk; gross versus net returns; horizon and currency consistency; evidence versus interpretation; diversification versus merely owning more things; entry versus management; sensitivity versus forecasting; and decision quality versus realised outcome.

Education content needs a stable identifier/version and domain review. AI may explain or adapt it to the user's level but should not silently rewrite deterministic definitions or formulas. Do not use inferred literacy or wealth as a reason to hide material risks.

A presenter mode can demonstrate one node change at a time while preserving the actual framework. Exported teaching examples must retain synthetic labels.

## 13. AI assistance and division of responsibility

### 13.1 Main agent

Understands the broad task; selects or builds a framework; researches evidence; helps formulate assumptions; explains methods; challenges inconsistencies; and proposes revisions. Uses validated application operations. It can revise this product's templates and design during development; client-side operation is more constrained than developer authority.

### 13.2 Optional Jev / typed semantic assessment

Useful for bounded questions such as whether a supplied passage explicitly changes an earlier outlook, whether a passage addresses the requested period, or which of several candidate evidence items fits a node. The question definition and permissible outcomes are part of the versioned assessment contract.

Jev is not needed for arithmetic, exact lookups, truth already known from structured data or every input change. It should not generate the graph, invent return distributions, declare broad investment merit or decide what permissions a user has.

The previously discussed phrase “do not use Jev for extraction” is best understood as a design boundary against unconstrained generation. The official TypeSafe guidance also describes selecting among candidate values/spans prepared by code. Such bounded selection remains possible, with candidate coverage checked; the product is not permanently limited to one demo's use cases.

### 13.3 Application code

Validates state, computes values, resolves applicable conditions, applies precedence, preserves unknowns, records results and renders the interface. It decides whether a proposed assessment can be consumed under the configured policy.

### 13.4 User

Provides goals, preferences and decisions that cannot be legitimately inferred. Can challenge the framework, change agreed assumptions/policies, keep an alternative course and decide whether a monitored process is wanted. Existing standing instructions should be honoured without repetitive requests to confirm them.

## 14. Sensitivity, alternatives and information priorities

The first useful sensitivity capability is transparent one-at-a-time scenario editing, not a black-box optimisation score.

For supported deterministic numeric criteria, show the comparison boundary and the difference from it, with correct units and operator. A strict “greater than” boundary cannot be described as passing at equality. A slider crossing a boundary shows a rule change, not a probability of real-world success.

A later extension can identify combinations of assumptions that change an outcome, but should display feasibility constraints and dependencies. It must not suggest “fixing” a failed case by quietly relaxing the user's policy.

Research priorities can begin with deterministic labels: missing required input; evidence too old for its declared purpose; conflicting sources; or an input close to a decision boundary. Do not call this a formal value-of-information calculation unless the utility model, probabilities and research costs are actually defined.

Alternative comparisons should retain the do-nothing/wait option and expose incompatible bases. Waiting is not assumed to be riskless or costless; record opportunity cost when a supported model exists rather than fabricate a universal value.

## 15. Monitoring, meaning changes and replay

Monitoring is a later integration lane built on the same evaluation contract. It requires an explicit source, retrieval mechanism, cadence, freshness rule, decision recipe and notification destination. Browser polling for changed local JSON is not evidence collection and does not create an always-on watcher.

A watcher can fetch changed source material, eliminate exact duplicates, ask a narrow semantic question, evaluate the case and record the result. A notification should explain the changed observation, relevant node, rule result and unresolved issue. It should not issue an unqualified investment instruction.

Use change hashes, event identities and deduplication. Hysteresis may reduce oscillation in soft semantic review signals, but must not silently delay a hard-condition event or hide service failure. Quiet notifications must not conceal an observable retrieval error in the workbench.

Replay uses the recorded framework, input snapshot, evaluation clock and stored assessment; it is not a fresh model call. A new model assessment is a new evaluation, separately labelled.

## 16. Learning and decision review

Retain what was known, the assumption basis, the alternatives considered, the framework result and the user's disposition. Later record actual outcomes separately.

The review experience should ask whether the evidence was adequate, assumptions were explicit, hard constraints were respected, alternatives were considered and the process was followed. It should not label every winning outcome a good decision or every loss a bad process.

Advanced research features can later support calibration, forecast tracking and point-in-time replay, but only with sufficient labelled observations and clear sampling limitations. Do not imply that a few successful examples validate an investment strategy or AI model.

## 17. Advanced concepts: extension path, not first-release burden

| Capability | User benefit | Preconditions and boundary |
|---|---|---|
| Richer scenario distributions and stress tests | See asymmetric downside and combinations of assumptions | Explicit scenario model, common units/horizon, documented dependence and cost treatment |
| Position-risk and sizing modules | Connect a stated risk budget to instrument exposure | Instrument-specific loss model, fees, gaps/liquidity and portfolio scope; no universal Kelly default |
| Monte Carlo / path simulation | Explore distributional/path implications | Declared stochastic model, dependence, seed, sample count and convergence diagnostics; no fabricated forecasts |
| Bayesian updating | Make explicit how new evidence changes stated beliefs | Named hypothesis, prior and likelihood basis; avoid double-counting correlated evidence |
| Portfolio interaction modules | Examine aggregate exposures and stress effects | Compatible holdings, data quality, capital coordination and declared covariance/stress assumptions |
| Multi-criteria preferences | Make trade-offs visible | Separate compensating preferences from non-compensable hard constraints; transparent scales and weights |
| Research/monitoring recipes | Reuse narrow evidence assessments | Versioned questions, candidate coverage, labelled evaluation examples and operational ownership |

These modules should expose their assumptions through the same node/evidence model and deterministic contracts. Do not add an arbitrary formula interpreter or universal strategy builder merely to claim extensibility.

## 18. Privacy, portability and integration posture

Keep client cases private by default. A public source-code repository is not a suitable default location for portfolios, downloaded proprietary research, model credentials or local capability URLs. Static exports can contain sensitive data even if they have no network connection.

The first delivery should be usable locally without a new account system, cloud migration or always-on server. Existing IQ Wealth/Vault distribution and knowledge mechanisms can be reused after their actual interfaces and entitlement checks are verified. Do not assume a successful private download or installed-client launch from a development-container test.

Export categories should be explicit: complete private working record; sanitised demonstration/template; static evaluation snapshot; and what-if scenario. Every export retains framework version, as-of/evaluation dates, scope, synthetic status and important unresolved conditions. A static snapshot must not appear to be live.

Later embedded/hosted versions should reuse the same semantic contracts and evaluator, with deliberate identity/isolation and sharing design. They are not prerequisites for proving the product.

## 19. Product quality and measurement

Evaluate with representative tasks, not just visual polish:

- Can the user identify the decisive condition and a material unknown without assistance?
- Can they distinguish a saved fact, an assumption, a policy and an AI assessment?
- Can they explain why changing an input changed the route?
- Can they explore and revert a scenario without corrupting the saved case?
- Does the assistant create a usable case without repeatedly writing renderer code or asking redundant questions?
- Can an existing case be reopened and reviewed with correct provenance and lifecycle?

Collect task completion, comprehension errors, accidental saves, repeated clarification loops, conflict/recovery failures, rendering failures, and model abstention/correction rates. Model latency/cost and development speed matter, but do not replace correctness or client comprehension. Telemetry should be local/opt-in as appropriate and avoid collecting client research by default.

Pilot targets and thresholds belong in the delivery plan as provisional engineering/product goals, not claims that have already been measured.

## 20. Source basis and review limits

The baseline product direction is grounded in this conversation and these reviewed resources:

- [N9 experiment notes at the reviewed commit](https://github.com/N9ALV/archify/blob/307fc4b353e75eb23d620c727891515955fa3aa3/docs/interactive-decision-workbench-experiment.md): node-owned controls, semantic JSON, what-if separation and decision semantics.
- [Conditional decision example](https://github.com/N9ALV/archify/blob/307fc4b353e75eb23d620c727891515955fa3aa3/experiments/interactive-decision-workbench/examples/conditional-decision.json) and [position-review example](https://github.com/N9ALV/archify/blob/307fc4b353e75eb23d620c727891515955fa3aa3/experiments/interactive-decision-workbench/examples/position-review.json).
- [HTML interaction prototype](https://github.com/N9ALV/archify/blob/307fc4b353e75eb23d620c727891515955fa3aa3/experiments/interactive-decision-workbench/examples/investment-node-controls.html): useful demonstration, not a generic JSON runtime.
- [Archify product principles](https://github.com/N9ALV/archify/blob/307fc4b353e75eb23d620c727891515955fa3aa3/PRODUCT.md), [skill](https://github.com/N9ALV/archify/blob/307fc4b353e75eb23d620c727891515955fa3aa3/archify/SKILL.md) and [package manifest](https://github.com/N9ALV/archify/blob/307fc4b353e75eb23d620c727891515955fa3aa3/archify/package.json).
- [ShapeShift question definitions](https://github.com/anishfn/shapeshift/blob/main/src/lib/jev/questions.ts): typed questions and independent speculative signals as a reference pattern, not an investment engine.
- [Official TypeSafe skill](https://github.com/typesafe-ai/skills/blob/main/skills/typesafe-ai/SKILL.md), reviewed blob `0109513f9656917dc93cbc5ecddfca465a53ce66`: bounded judgments, independent questions, uncertainty, candidate selection and application-owned control flow. Live documentation endpoints did not load in this review; confirm current SDK/API details before implementation. No provider pricing, latency or version guarantee is asserted here.
- Earlier private project artefacts `skill-iq-decision-workbench.md` and `iq-decision-workbench-test-report.md`, dated 14 September 2026, were read from the user's Library. They describe a separate 0.1.0 local pilot, four templates and reported tests, with explicit native-browser/Windows acceptance limitations. Its code/package was not inspected or imported in this handover. Locate an authorised existing copy before deciding what to reuse; do not presume it is the Archify implementation or republish private distribution details.

This is a source-and-design review, not a completed runtime, investment-validation, security-certification or legal review. The purpose of the accompanying plan is to turn the concept into inspectable implementation increments while allowing the IDE lead and Adam to improve it.