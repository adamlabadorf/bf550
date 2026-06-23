---
title: "Learning Objectives"
permalink: /learning-objectives/
toc: true
toc_sticky: true
---

By the end of BF550, you will be able to:

## Applied statistics & ML reasoning

1. **Frame** a biological question as a statistical or machine-learning problem, and state
   what kind of answer the question is actually asking for.
2. **Distinguish the major classes of ML algorithms** and explain how they differ in
   assumptions, inputs, outputs, and the kind of question they answer:
   - supervised vs. unsupervised learning
   - classification vs. regression
   - clustering and other unsupervised structure-finding
   - feature-importance / interpretable methods (e.g. decision trees, random forests)
   - dimensionality reduction
3. **Choose an appropriate method** for a given problem and dataset, and justify the choice —
   including recognizing when *not* to use a complex method.
4. **Reason about model behavior** — overfitting/underfitting, the bias–variance tradeoff,
   data leakage, and why a model's reported performance may not generalize.
5. **Interpret and critique results** — read evaluation metrics (accuracy, precision/recall,
   ROC/AUC, clustering validity) and judge whether a result is meaningful for the biology.

## Code literacy

6. **Read a code snippet and accurately describe what it does**, including edge-case
   behavior — without executing it.
7. **Recover a specification** from an implementation and its tests: state inputs, outputs,
   types, and invariants precisely enough that another person could re-implement it.
8. **Read code as design** — explain how a program is decomposed and organized to solve the
   problem, identify where complexity and risk live, and assess whether the design fits a
   larger analysis pipeline.
9. **Identify underspecification and gaps** — find behaviors that a spec or test suite fails
   to pin down, and propose tests or clarifications.

## Working with generative AI / coding agents

10. **Decompose a problem into design → spec → tests *before* generating code**, and direct a
    coding agent to satisfy those constraints.
11. **Verify agent-generated code** — write example-based, synthetic, and property-based
    tests with hand-calculated expected values; diagnose whether a failure originates in the
    spec, the tests, or the generated code.
12. **Exercise engineering judgment** — critique an implementation for correctness,
    efficiency, and composability, and decide what is worth fixing vs. deferring.

## Disciplinary grounding

13. **Apply all of the above to real molecular-biology and genomics problems**, connecting a
    statistical/ML method to the biological question it serves and to published tools and
    workflows in the field.
