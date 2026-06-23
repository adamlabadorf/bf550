---
title: "Assignments: Design → Spec → Test → Implementation"
permalink: /assignments/
toc: true
toc_sticky: true
---

Every coding lab and assignment in BF550 treats a problem as four connected pieces:

1. **Design** — how the problem breaks down: the interfaces, the data flow, where the
   complexity lives.
2. **Specification** — the precise contract: inputs, outputs, types, invariants, edge cases.
3. **Tests** — executable expectations, with expected values you've worked out by hand.
4. **Implementation** — code that satisfies the spec and passes the tests.

Each assignment **gives you some of these pieces and asks you to produce the one that's
missing.** That keeps the focus on a specific skill — and it's why you can use a coding agent
freely: the part you're graded on (the design, the spec, the tests, the critique) is exactly
the part an agent can't do for you.

## The four exercise types

### Type A — Spec + Tests → Code

You're given a complete specification and a test suite. Produce an implementation that passes
all the tests, **annotate every non-trivial line** so you can explain what it does, and keep
a **failure log**: for each test that failed along the way, note whether the problem was in
the spec, the tests, or the generated code.

*You're practicing:* implementation and directing a coding agent.

### Type B — Spec + Code → Tests

You're given a specification and a working implementation. Write a test suite that includes:

- **example-based tests** with **hand-calculated expected values shown in the docstring**;
- at least one **synthetic test** — an input you construct to expose a specific behavior, with
  your reasoning;
- at least one **property-based test** — an invariant that should hold for any valid input;
- at least one **documented expected failure** identifying a known limitation.

The hand-calculated values are the point: writing them means you understand the problem
yourself.

*You're practicing:* verification, and turning biological intuition into tests.

### Type C — Code + Tests → Spec

You're given a working implementation and its tests. Write the specification: describe the
inputs, outputs, and types precisely enough that someone could re-implement it without seeing
the code, explain the reason behind **every edge case** the tests cover, point out **at least
two behaviors the tests don't cover** (and propose tests for them), and note anything
ambiguous in the current implementation.

The gap analysis — what's *not* pinned down — is the most valuable part.

*You're practicing:* close reading, recovering intent, and spotting underspecification.

### Type D — All three → Critique & Optimize

You're given a complete, correct implementation with its spec and tests. Write a critique on
three levels:

- **Correctness** — does it satisfy the spec even in cases the tests miss? Each gap you find
  needs a proposed test.
- **Efficiency** — does it do unnecessary work? Reason about this *from reading the code*
  (e.g. list vs. generator, recomputation, running counts), not from benchmarking.
- **Composability** — would it fit into a larger pipeline? Think about its interface and how
  it would run over many samples.

Summarize your findings in a table: for each issue, its impact, the effort to fix, and
whether the fix would break existing behavior. Deciding what's worth fixing is part of the
exercise.

*You're practicing:* engineering judgment and reasoning about tradeoffs.

## Where these ideas come from

The framework borrows from established software-engineering practice — recast as ways of
*thinking*, not coding mandates:

- **Test-Driven Development (TDD):** express the behavior you want as tests before the
  implementation exists.
- **Behavior-Driven Development (BDD):** phrase tests in plain, domain-meaningful terms
  ("a pure-GC window has GC fraction 1.0").
- **Design-Driven Development:** make your interface and decomposition choices explicit and
  reviewable before committing to code.

## Using a coding agent on assignments

- **Your design, spec, and tests are your own work** — these aren't delegated to an agent.
- **You may have an agent generate the code**, but you're accountable for explaining it
  (line-level annotation) and for diagnosing every test failure before you accept the output.
- **The failure log is graded** — it shows your refine-and-verify process.

The habit to build: *constrain the problem first (design → spec → tests), then generate the
code, then verify it.* See the [assessment & AI policy](https://bu-bioinfo.github.io/bf550/assessment/)
for the AI level that applies to each assignment.
