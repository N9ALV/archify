# Interactive decision workbench experiment

## Why this was explored

A practical investment-decision use case exposed an interesting extension to Archify: the diagram can become the decision interface itself.

Instead of a separate form controlling a diagram, bounded inputs can live **inside the nodes that own the criteria**:

- `Thesis intact?` → Yes / No.
- `Expected return > required return` → numerical comparison.
- `Portfolio exposure <= maximum exposure` → numerical constraint.
- Post-entry monitoring → hard exit, re-evaluate or continue monitoring.

The broader process used a DEEP-style flow:

**Discover → Educate → Evaluate → Perform → Monitor / Re-evaluate**

## Positive results

### 1. Ordinary Archify already maps the process well

The conventional source in [`examples/investment-decision.architecture.json`](../examples/investment-decision.architecture.json) uses existing Architecture components, boundaries, connections, cards and guided views to show evidence, research, valuation, risk, portfolio fit, implementation and feedback.

That is useful even without controls.

### 2. Node-level controls are substantially clearer than a detached control panel

The working prototype in [`experiments/interactive-decision-workbench/examples/investment-node-controls.html`](../experiments/interactive-decision-workbench/examples/investment-node-controls.html) places Yes/No and numerical inputs inside the relevant nodes and derives the active route from the current values.

This keeps the visual model and decision model aligned.

### 3. The agent should populate semantic data, not write UI code

A standard `yes_no` node should know how to render its toggle and expose its outcomes. A `number_compare` node should know how to render values, units and its operator.

The agent should provide values, labels and relationships—not CSS, event listeners or connector geometry.

### 4. Durable state and what-if state should be separate

For a serious local workbench, JSON should remain the source of truth. Browser edits are best treated as temporary what-if state until deliberately saved.

That produces a clean split:

```text
decision JSON
    ↓
validation + deterministic engine
    ↓
standard renderer
    ↓
local browser
```

### 5. Browser-first is the right surface for wide decision diagrams

A normal browser tab gives these diagrams the width they need. A local, loopback-only host is preferable when separate JSON files need to be read dynamically.

## Lessons from failed or weaker attempts

### Fixed-position geometry collides easily

Early dashboard versions used hand-authored absolute positions. Variable node height then produced overlap, label collisions and connectors passing through unrelated content.

**Implication:** if this becomes a first-class Archify feature, node dimensions and routing must remain renderer-owned and measured after content is known.

### SVG `foreignObject` is a fragile way to retrofit controls

A first control prototype relied on SVG `foreignObject` and brittle DOM insertion points. Ordinary HTML controls anchored by a renderer contract were more reliable.

**Implication:** control placement should be first-class rather than post-hoc DOM surgery.

### Arbitrary graph-in-query-string is not a good general authoring format

URL parameters are useful for a known template and a handful of initial values. Encoding an arbitrary graph or Mermaid-like syntax into a URL is much more failure-prone.

**Implication:** use short URL parameters for template selection / initial values, or load a compact JSON record for larger workbenches.

## Candidate bounded vocabulary

A future typed extension could start small:

- `information`
- `yes_no`
- `number_compare`
- `range`
- `choice`
- `outcome`

Later, carefully bounded composition could add `all` / `any` groups.

Weighted scores and arbitrary executable formulas are poor first extensions: they are harder to validate, explain and keep truthful.

Example:

```json
{
  "id": "return_hurdle",
  "kind": "number_compare",
  "stage": "evaluate",
  "label": "Expected return hurdle",
  "left": {
    "label": "Expected",
    "value": 14,
    "unit": "%"
  },
  "operator": ">",
  "right": {
    "label": "Required",
    "value": 10,
    "unit": "%"
  },
  "outputs": {
    "pass": "portfolio_fit",
    "fail": "watch"
  }
}
```

## Decision semantics matter as much as rendering

The investment examples surfaced several generally useful rules:

1. **Unknown is not false or zero.** Missing input should stay unresolved.
2. **Policy thresholds are not observations.** Keep provenance distinct.
3. **Entry failure is not automatically an exit.** Lifecycle context changes the meaning of a failed gate.
4. **Hard conditions may override soft review triggers.** Precedence must be authored, not inferred from colour.
5. **A pass only means the configured rules pass.** It is not evidence of investment quality, approval or execution.
6. **What-if browser edits should not silently mutate durable state.**
7. **Feedback loops should represent review relationships, not uncontrolled recursive automation.**

## Architectural choices if taken into Archify core

This experiment should remain separate until there is a deliberate design for:

- whether `decisionflow` becomes a sixth diagram type or controls become an optional interaction layer;
- typed control definitions and validation diagnostics;
- renderer-owned layout for variable-height controls;
- canonical versus temporary viewer state;
- export semantics;
- accessibility and keyboard behaviour;
- whether durable decision state belongs in Archify or remains application-owned.

Until then, the files in `experiments/interactive-decision-workbench/` are evidence and working references, not claims about Archify 2.15.
