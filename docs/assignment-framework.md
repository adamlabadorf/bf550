# Assignment Framework: Design → Spec → Test → Implementation

Every coding assignment and lab in BF550 is built on a four-component view of a problem:

1. **Design** — how the problem is decomposed: interfaces, data flow, where complexity lives.
2. **Specification** — the precise contract: inputs, outputs, types, invariants, edge cases.
3. **Tests** — executable expectations with hand-calculated expected values.
4. **Implementation** — code that satisfies the spec and passes the tests.

The pedagogical move (adapted from the
[bf550-brainstorming](https://github.com/bu-bioinfo/bf550-brainstorming) repo) is that an
exercise **provides some of these components and asks the student to produce the missing
one(s).** This isolates a specific skill and makes agent use safe: the student's graded
product is the part a coding agent cannot supply for them.

This is also why the framework works across our wide skill range. **Spec writing, test
writing, and critique are novel to nearly every student regardless of Python background**,
so they level the field. Implementation can be scaffolded for novices and delegated to an
agent by experts *without changing what is being assessed.*

## The four exercise types

### Type A — Spec + Tests → Code

Given a complete spec and a test suite, produce an implementation that passes all tests.

**Deliverables:** the implementation, a **line-level annotation** of every non-trivial line,
and a **failure log** documenting, for each test that failed during development, whether the
failure originated in the spec, the tests, or the generated code.

- **Primary skill:** implementation, agentic tool use.
- **Where:** early (orientation). AIAS Level 4 — agent may write the code; annotation +
  failure log are the student's accountable product.

### Type B — Spec + Code → Tests

Given a complete spec and a working implementation, produce a test suite containing:

- **Example-based tests** with **hand-calculated expected values shown in the docstring**.
- At least one **synthetic test**: an input constructed to expose a known behavior, with
  rationale.
- At least one **property-based test**: an invariant that must hold for any valid input.
- At least one **documented expected failure** identifying a known limitation.

- **Primary skill:** verification; turning biological intuition into tests.
- **Enforcement:** a test without a worked expected value in its docstring is not accepted.
  This is the component an agent cannot produce without the student already understanding
  the problem.
- **Where:** verification-focused weeks.

### Type C — Code + Tests → Spec

Given a working implementation and its tests, produce a specification that:

- Describes inputs, outputs, and types precisely enough to re-implement without the code.
- Explains the design decision behind **every edge case** the tests cover.
- Identifies **at least two behaviors the tests do not cover** and proposes tests for them.
- Summarizes ambiguities / underspecified behaviors in the current implementation.

- **Primary skill:** critical reading; spec recovery; identifying underspecification.
- **Grading:** the **gap analysis is weighted more heavily than the spec itself** — finding
  what's underspecified shows deeper engagement than a complete-but-unsurprising spec.
- **Where:** the core code-literacy weeks.

### Type D — All three → Critique & Optimize

Given a complete, correct implementation with spec and tests, produce a critique across
three layers:

- **Layer 1 — Correctness:** does it satisfy the spec in cases the tests don't cover? Each
  gap requires a proposed test.
- **Layer 2 — Efficiency:** unnecessary work, memory footprint, asymptotic behavior —
  reasoned **from reading the code, not from benchmarking** (e.g. list vs. generator,
  redundant recomputation, running counts for sliding operations).
- **Layer 3 — Composability:** does it fit into a larger pipeline? Function-level design
  (interfaces, parameterization) and deployment-level design (multi-sample drivers, CLI
  entry points, parallel/cluster execution, environment documentation).

- **Primary skill:** engineering judgment, tradeoff reasoning.
- **Deliverable:** a **summary table** stating, per issue, its impact, the effort to fix, and
  whether the fix is breaking. Deciding what to fix vs. defer is part of the exercise.
- **Where:** later weeks; integrates everything.

## Mapping to engineering disciplines

| Discipline | How the framework uses it |
|---|---|
| **Test-Driven Development (TDD)** | Tests express desired behavior before/independent of implementation (Types A, B). |
| **Behavior-Driven Development (BDD)** | Tests are phrased in domain-meaningful, observable terms ("a pure-GC window has GC fraction 1.0"). |
| **Design-Driven Development** | Design & spec are explicit, reviewable artifacts produced before code is accepted (Types C, D; all designs). |

## Biological-grounding requirement

**Every exercise uses a problem whose correct answer is verifiable from domain knowledge
without running any code.** This is what makes Type B assessable and what connects the
framework to students whose primary background is biology.

- **Good fits** (answer checkable by hand from biology): FASTA/FASTQ parsing, reverse
  complement, codon translation, GC content, genomic interval overlap, alignment summary
  stats, k-mer / Naive Bayes classification.
- **Poor fits** (require running code to verify): sorting algorithms, abstract data
  structures, string puzzles. **Do not use these.**

## Agentic-tool policy (summary)

- **Design, spec, and tests are always the student's intellectual product** and cannot be
  delegated.
- **Code may be agent-generated**, but the student is accountable for line-level annotation
  and for diagnosing every test failure before accepting output.
- **The failure log is graded.** It makes the iterative refine-and-verify loop visible.

The rule of thumb: *constrain first (design → spec → tests), then generate, then verify.*
Generating code first and retrofitting a rationale inverts the process and produces nothing
verifiable. Full policy and AIAS mapping: [assessment-and-ai-policy.md](assessment-and-ai-policy.md).

> **GAP:** define the standard deliverable bundle and file layout per lab (e.g.
> `spec.md`, `test_*.py`, `impl.py`, `annotation.md`, `failure-log.md`), a rubric per type,
> and the toolchain/runtime students use (Python version, test runner, provided agent).
