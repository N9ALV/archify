# N9 Archify experiments

This fork retains Archify's upstream renderer and validation model while keeping selected N9 experiments separate from the stable core.

## Interactive decision workbench

The current experiment explores a useful extension beyond static/explorable diagrams: **renderer-owned controls inside decision nodes, with agent-maintained JSON state and deterministic outcome logic**.

Start here:

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

These files are experiments. Interactive controls are **not part of Archify 2.15's typed JSON schema** and should not be confused with a validated upstream feature.
