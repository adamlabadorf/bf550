# Assignment Framework — Authoring Guidance (INTERNAL)

> **Internal planning document — not published to the course site.** The student-facing
> version is the **"Assignments"** page (`docs/assignment-framework.md`, `/assignments/`).
> This file holds the guidance for whoever is *writing* the assignments.

## Why the framework works across our skill range

Spec writing, test writing, and critique are **novel to nearly every student regardless of
Python background**, so they level the playing field. Implementation can be scaffolded for
students who need it and delegated to a coding agent by students who don't — *without
changing what the exercise actually assesses.* This is what lets one course serve both the
rudimentary and the highly skilled programmer.

## When to use each type (sequencing)

- **Type A — Spec + Tests → Code:** early (orientation); agent may write the code while the
  annotation + failure log are the accountable product. AIAS Level 4.
- **Type B — Spec + Code → Tests:** verification-focused weeks. **Enforcement:** a test
  without a worked, hand-calculated expected value in its docstring is not accepted — this is
  the component an agent cannot produce without the student already understanding the problem.
- **Type C — Code + Tests → Spec:** the core code-literacy weeks. **Grade the gap analysis
  more heavily than the spec itself** — finding underspecification shows deeper engagement
  than a complete-but-unsurprising spec.
- **Type D — All three → Critique:** later weeks; integrates everything. The summary table
  (impact / effort / breaking?) is the primary deliverable.

## Biological-grounding requirement (author rule)

**Every exercise must use a problem whose correct answer is verifiable from domain knowledge
without running any code.** This is what makes Type B assessable and connects the framework
to biology-first students.

- **Good fits** (checkable by hand from biology): FASTA/FASTQ parsing, reverse complement,
  codon translation, GC content, genomic interval overlap, alignment summary stats,
  k-mer / Naive Bayes classification.
- **Poor fits** (require running code to verify): sorting algorithms, abstract data
  structures, string puzzles. **Do not use these.**

## Open decisions

- **GAP:** define the standard deliverable bundle and file layout per lab (e.g. `spec.md`,
  `test_*.py`, `impl.py`, `annotation.md`, `failure-log.md`), a rubric per type, and the
  toolchain/runtime (Python version, test runner, provided agent). Tracked in
  [issue #5](https://github.com/bu-bioinfo/bf550/issues/5).

## Templates

Authoring templates live in [`internal/templates/`](templates/): the TILT assignment template
and the check-in quiz template.
