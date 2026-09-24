# Interactive decision workbench

Experimental N9 fork material for conditional, input-bearing decision diagrams.

## Included examples

- `examples/investment-node-controls.html` — self-contained browser prototype with controls inside nodes.
- `examples/conditional-decision.json` — compact pre-entry decision structure.
- `examples/position-review.json` — post-entry example separating hard exit from softer re-evaluation.

Open the HTML file directly in a browser. It has no external dependencies.

## Relationship to Archify

The examples borrow Archify's visual/semantic ideas, but the control vocabulary is not part of the Archify 2.15 schema. Keep this folder experimental until the schema, validation, layout and state semantics are deliberately designed.

The important pattern is:

```text
semantic JSON → validator/engine → renderer-owned nodes + controls → browser
```

Agents should populate semantic values, not author geometry or JavaScript per decision.

For a normal Archify-only rendering of the same investment process, see `../../examples/investment-decision.architecture.json`.
