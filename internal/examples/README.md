# Example Lab Materials (INTERNAL — DRAFTS)

> **Not published, not final, not authored against a settled spec.** These are *playable drafts*
> written to make the lab flow concrete so we can react to it. They implement the structure in
> [`../lab-computational-thinking-framework.md`](../lab-computational-thinking-framework.md).

| File | Week | Seat | Term position | Shows |
|---|---|---|---|---|
| [`week-01-lab.md`](week-01-lab.md) | 1 — Course intro / GC sliding window | **Implementer** (writes CODE) | **First lab** | Introduces the whole machinery; productive uncertainty as an *absence in the spec*; the agent-decisions exercise |
| [`week-04-lab.md`](week-04-lab.md) | 4 — Naive Bayes / rRNA classification | **Verifier** (writes TESTS) | Early | Full scaffolding, paired phase 1, hand-calculable tests |
| [`week-10-lab.md`](week-10-lab.md) | 10 — Clustering / scRNA-seq | **Reverse engineer** (writes SPEC) | Middle–late | Reduced scaffolding, individual phase 1, a multi-hole extension |

Read in that order, the three show the intended arc: Week 1 explains the machinery and plants
*absences*; Week 4 plants *arguable choices* in working code; Week 10 plants *silent defects* and
expects students to distrust what they are given.

Each file is laid out in the order a student meets it — Monday problem statement, phase-1
worksheet, the gate, Wednesday reveal with the real materials inline, divergence analysis, seat
work, Friday share-out — with **instructor notes fenced off at the end**, including where the
productive uncertainty is planted.

## What to poke at when reading these

1. **Does the Monday problem statement leave the decomposition to the student**, or does it leak?
2. **Is 25–30 minutes plausible** for the phase-1 worksheet as written?
3. **Is the planted productive uncertainty findable but not gotcha-ish?**
4. **Does the divergence analysis have enough to bite on**, or does it read as busywork?
5. **Does the Week 10 example feel meaningfully different from Week 4**, or has the structure
   flattened into a template that ignores where students are in the term?
