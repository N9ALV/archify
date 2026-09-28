# IQ Decision Workbench

A persistent, browser-first decision-support workbench for investors and traders: explicit questions, evidence, assumptions, constraints and scenarios, presented through interactive decision nodes with contextual education and AI assistance.

**Status:** detailed living specification and IDE handover, prepared 28 September 2026. This documentation does not claim the proposed runtime or integrations are already implemented.

## Start here

| Document | Read it for |
|---|---|
| [IDE handover](IDE-HANDOVER.md) | Taking over as implementation lead, working with Adam, implementation discretion, avoiding unnecessary permission loops, and the first executable slice |
| [Product specification](PRODUCT-SPEC.md) | Product purpose, users, full journeys, interface surfaces, four initial template families, education, AI roles and advanced extension path |
| [Technical specification](TECHNICAL-SPEC.md) | Semantic records, node contracts, evaluation/lifecycle logic, unknown states, provenance, scenarios, persistence, optional Jev integration and operational boundaries |
| [Delivery and acceptance](DELIVERY-AND-ACCEPTANCE.md) | Source-review findings, reuse opportunities, milestones, requirements traceability, concrete acceptance fixtures and demonstration sequence |

## The essential idea

The same versioned semantic framework should drive the interface, deterministic calculations, rule trace and saved evaluations. Users and agents can inspect it, revise it and explore what would change the result. The renderer owns layout and controls; the main agent helps build/explain/research the framework; an optional typed semantic model supplies narrow evidence assessments; application code owns calculations and control flow.

The product should help someone understand **what matters, what is missing, why a result follows, what would change it and what changed since the last review**. It is not simply a flowchart, a universal investment score or an automatic trading system.

## Handover authority

Adam remains the product owner. The IDE agent becomes the design/implementation lead when assigned the build. These documents are a detailed revisable baseline, not a frozen plan or a requirement to request approval for every engineering decision. Follow Adam's current direction, use reasonable discretion within scope, keep changes recoverable and report actual verification. See the handover for the full operating guidance and a ready-to-use brief.

## Reviewed starting point

The repository baseline was `307fc4b353e75eb23d620c727891515955fa3aa3`, including the [original experiment notes](../interactive-decision-workbench-experiment.md), [HTML controls prototype](../../experiments/interactive-decision-workbench/examples/investment-node-controls.html), [pre-entry JSON](../../experiments/interactive-decision-workbench/examples/conditional-decision.json), and [live-position JSON](../../experiments/interactive-decision-workbench/examples/position-review.json).

The HTML is a hard-coded interaction demonstration, not a generic evaluator of the JSON examples. The review also located documentation for a separate earlier local workbench pilot; its code should be inspected for reuse when an authorised copy is available. It was not imported or runtime-tested as part of this specification.

## Suggested first increment

Build one complete manual-input case with semantic records driving node controls and deterministic evaluation, correct unknown/zero/false behaviour, inspectable evidence, separate what-if state, validated persistence/reopen and an actual browser launch. Then expand through the other templates and richer assistance. Jev credentials, cloud hosting, autonomous monitoring and advanced quantitative modules are not prerequisites for that first useful product.

Source links and review limitations are in the product specification. The implementation status and acceptance evidence should be updated by the IDE lead as the product develops.
