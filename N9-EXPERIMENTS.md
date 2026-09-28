# N9 Archify experiments

This fork retains Archify's upstream renderer and validation model while keeping selected N9 experiments separate from the stable core.

## IQ Decision Workbench — product specification and IDE handover

The interactive decision-workbench direction now has a detailed, living product specification. It maps the client experience, contextual education, deterministic decision semantics, optional Jev assessments, persistence/scenarios, integrations, delivery stages and acceptance fixtures.

**Start with the [specification index](docs/decision-workbench/README.md).**

- [IDE lead handover](docs/decision-workbench/IDE-HANDOVER.md): take over the implementation lead role, iterate with Adam, and exercise ordinary engineering discretion during long-running tasks.
- [Product specification](docs/decision-workbench/PRODUCT-SPEC.md): purpose, user journeys, interface, templates, education and extension path.
- [Technical specification](docs/decision-workbench/TECHNICAL-SPEC.md): contracts, evaluation, provenance, state, persistence and integration design.
- [Delivery and acceptance](docs/decision-workbench/DELIVERY-AND-ACCEPTANCE.md): reviewed gaps, reuse opportunities, milestones, test fixtures and concrete demonstrations.

**This is a handover, not a frozen plan.** Adam remains the product owner; the IDE agent becomes the design/implementation lead when assigned the build. The agent should refine the design with Adam, make sensible reversible decisions within scope, and deliver working increments without unnecessary permission loops. The documents describe intended behaviour, not a claim that all capabilities are already implemented or a requirement to build the entire roadmap before a usable pilot.

## Original interactive decision workbench experiment

The original experiment explores a useful extension beyond static/explorable diagrams: **renderer-owned controls inside decision nodes, with agent-maintained JSON state and deterministic outcome logic**.

Historical starting points:

- [Experiment notes](docs/interactive-decision-workbench-experiment.md)
- [Conventional Archify investment map](examples/investment-decision.architecture.json)
- [Interactive node-controls prototype](experiments/interactive-decision-workbench/examples/investment-node-controls.html)
- [Conditional decision JSON](experiments/interactive-decision-workbench/examples/conditional-decision.json)
- [Existing-position review JSON](experiments/interactive-decision-workbench/examples/position-review.json)

### Direction worth exploring

```text
agent/user intent
      ↓
small decision JSON
      ↓
validator + standard node vocabulary
      ↓
renderer-owned layout, controls and path state
      ↓
local browser
```

This avoids asking an agent to repeatedly author HTML, SVG geometry, JavaScript or long encoded URLs. The agent changes semantic values; the renderer owns presentation and interaction.

These files are experiments. Interactive controls are **not part of Archify 2.15's typed JSON schema** and should not be confused with a validated upstream feature. The new specification preserves that distinction and maps how to develop a reusable workbench from the concept.
