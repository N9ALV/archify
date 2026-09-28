# IQ Decision Workbench — IDE lead handover

**Prepared:** 28 September 2026.  
**Product owner:** Adam.  
**Purpose:** transfer the concept, source review and working product specification to the IDE agent that will lead design and implementation with Adam.

## 1. Read this before interpreting the specification

**This is a handover, not a frozen architecture or an approval hierarchy.** Adam explicitly wants the IDE agent to become the lead from this point, iterate with him and complete substantial long-running assignments with discretion and proactivity.

The previous assistant is not an ongoing approval authority. Do not treat its proposed field names, module boundaries, milestone order, preferred implementation or length of documentation as instructions to stop and seek permission before ordinary progress.

Adam's current directions supersede working defaults in these documents. When a better design emerges, propose it when discussion is useful, make sensible reversible decisions during an assigned task, and update the documentation. The goal is a useful product, not compliance theatre around a plan.

This documentation handover itself does not launch an IDE task or deploy anything. Once Adam gives the implementation assignment, use the scope of that assignment and existing tool permissions to proceed.

## 2. What we are trying to build

A persistent browser workbench that lets ordinary investors and traders work with explicit decision logic, evidence, assumptions, risk constraints and scenarios, supported by contextual education and AI assistance.

Its value is not that AI can draw a flowchart. Its value is that the user can inspect what matters, see what is missing, understand why a result follows, explore what would change it, and return later to review the same reasoning.

One semantic specification should drive controls, calculations, rule traces and saved evaluations. The agent works with semantic records; the renderer owns layout. The deterministic engine handles arithmetic and rule logic. Jev is an optional bounded evidence-assessment method, not the engine, not the graph author and not an authority over investments or permissions.

Make the product useful without Jev first. Do not let its absence trivialise the eventual AI experience: contextual explanation, evidence gathering and framework construction by the main agent are central parts of the intended product.

## 3. Read order

1. [Product specification](PRODUCT-SPEC.md): purpose, audience, client journeys, four templates, education, AI roles and extension path.
2. [Technical specification](TECHNICAL-SPEC.md): proposed entities, evaluation semantics, state separation, persistence and integration contracts.
3. [Delivery and acceptance](DELIVERY-AND-ACCEPTANCE.md): baseline findings, milestones, traceability and concrete test fixtures.
4. Original [experiment notes](../interactive-decision-workbench-experiment.md) and the small prototype/examples when useful to understand the starting point.

Do not reread all reference material for every change. Use relevant sections after orienting yourself. Keep a concise current implementation status so a resumed session can continue without reconstructing the whole conversation.

## 4. Your discretion during an assigned build

Within the assigned scope, you are expected to:

- Inspect actual code, runtime and local state; identify differences from the reviewed commit and protect concurrent/uncommitted work.
- Reuse compatible existing code, restructure an experimental module, choose appropriate dependencies, refine contracts and improve weak wording or UI choices.
- Implement complete vertical slices including tests, persistence, usable controls, examples and actual launch instructions—not stop after another outline.
- Debug, refactor, repair tests and revise the plan when evidence shows a better route.
- Select reasonable reversible defaults where the product owner has not specified a detail; record material assumptions and continue.
- Complete the connected sub-tasks of a long-running assignment without asking for approval at each milestone heading.
- Checkpoint work, keep status current, and provide useful progress reports and a clear final handoff.

A milestone is a coherent delivery unit, not an automatic permission checkpoint. After finishing one, continue into the next relevant sub-task when that is within Adam's current assignment. Do not assume permission for an unrelated expansion merely because it appears somewhere in the roadmap.

## 5. Decisions to discuss versus details to resolve

Discuss a choice when it materially changes the user experience, product purpose, delivery model, costs or the scope Adam requested, or when information only he can supply is genuinely necessary.

Do not stop merely because a proposed schema field could have a better name, a renderer approach has two reasonable options, a development dependency is needed within normal authority, a test needs repair, or a future integration is not configured. Choose, explain briefly, implement and record.

Real boundaries remain: do not destroy unrelated work, expose private data, enable public access, incur new material costs, alter production services, or execute financial transactions without the relevant user authority. This is a distinction between consequential scope changes and ordinary engineering, not a new universal confirmation requirement.

When one capability is blocked, complete independent work. For example, unavailable Jev credentials should leave a tested adapter/mock/manual path and a clearly identified live-check gap, not a stalled core workbench.

## 6. How to interpret modelling requirements

Some distinctions are essential to a truthful product: missing versus zero/false; observation versus policy; model assessment versus fact; saved versus what-if state; entry versus management; predicate truth versus favourable outcome; and rule result versus execution.

Preserve those meanings. Their implementation is flexible. An unresolved input in a client case is a useful visible state, not a reason to stop development or refuse to create the framework. A warning about investment uncertainty is not a reason to withhold ordinary tools or bury the user in disclaimers.

Do not silently relax a client's policy to manufacture a favourable result. Conversely, do not use policy-protection language to block Adam from deliberately revising the product or a framework. Honour actual instructions and standing authority without making him reconfirm the same decision repeatedly.

Advanced concepts are part of the mapped vision, not obligations to build every module before demonstrating the basic product.

## 7. Avoid inherited instruction traps

The upstream `archify/SKILL.md` is primarily an artefact-authoring/delivery guide. Instructions such as freezing a validated artefact, limiting geometry repair rounds, not inspecting renderer internals before a first candidate, and fitting a static diagram to one screen should not be misapplied as permanent limits on engineering this new product.

For workbench development, inspect and modify relevant implementation when needed. Allow a readable contained canvas with node controls where appropriate. A previously delivered diagram's immutable receipt should remain meaningful, but new source revisions are normal development.

Preserve upstream functionality and provenance; isolate the experimental work initially if that makes regression safer. You may choose a new diagram type, adapter or dedicated renderer after assessing the code. These documents do not require a specific approach to win by default.

The older local pilot's guidance also separates routine observation updates from policy/lifecycle changes in a client's case. That is not a prohibition on the IDE lead changing templates, schemas or development fixtures as part of an authorised implementation task.

## 8. Suggested first substantive assignment

Orient against the current repository, inspect any readily available authorised earlier pilot, and build one end-to-end generic manual-input workbench:

- semantic case/template records drive both node controls and deterministic evaluation;
- unknown/false/zero, equality boundaries and adverse matched conditions are correct;
- evidence/provenance is inspectable;
- what-if changes are separate from durable state;
- a validated saved record can be reopened;
- an actual local browser launch works on the tested platform;
- relevant tests and one clear synthetic demonstration accompany the implementation.

Expand to the other templates and richer persistence/education according to the assigned scope. Do not make a new cloud service, live provider integration or total upstream migration a prerequisite for the first useful slice.

The earlier separate 0.1.0 pilot may already contain reusable engine/store/test work. Its skill and report were reviewed; its package was not inspected during this handover. Locate an authorised copy if readily available. Its absence is a reuse limitation, not a blocker or a reason to publish a protected package into this public fork.

## 9. Long-running task working style

Start with a short statement of the slice and assumptions. Work through it proactively. Keep changes recoverable and avoid accumulating unrelated scope. Test the affected behaviour, then run broader relevant regression at a meaningful integration point.

When repeated attempts do not improve the situation, change tactic: inspect a smaller reproduction, isolate the failing layer or select another reasonable approach. Do not spend a long run repeatedly issuing the same test or polishing documentation while a core interaction remains unusable.

Keep progress/status concrete: implemented, verified, not yet verified, and blocked for a specific reason. Distinguish an environmental test limitation from an implementation defect. Continue useful independent work rather than stopping the whole assignment.

At handoff, provide the commit, actual use/launch instructions, a runnable case, tests/evidence, known limitations and the recommended next slice. Do not claim native Windows/IQ Browser acceptance from a Linux injected-browser harness, or live model quality from mock tests.

## 10. Maintain the design rather than obeying obsolete prose

Update material changes in the relevant document and keep a small decision log if useful: decision, reason, alternatives, effect and verification. Record which assumptions were replaced by evidence.

Do not create an elaborate governance system for every small change. The product owner and implementation lead should be able to revise the direction conversationally and then continue working.

A useful opening message from the IDE lead would be a concise interpretation of the intended product and the first executable slice, not a request for blanket approval of every section of this specification.

## 11. Ready-to-use handover brief

> Take over as implementation lead for IQ Decision Workbench. Read `docs/decision-workbench/IDE-HANDOVER.md` and the linked product, technical and delivery specifications. Review the current repository and reuse any compatible existing pilot work that is readily available. Treat the documents as a detailed, revisable baseline, not a frozen plan. Work with me on material product decisions, but use your judgement and proceed proactively on routine design, implementation, debugging and testing within the assigned scope. Start with a runnable end-to-end manual-input workbench driven by semantic records, then build out the next useful slice. Preserve truthful decision semantics and existing work, avoid unnecessary permission loops, and deliver working checkpoints with actual verification and clear limitations.
