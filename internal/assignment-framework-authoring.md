# Assignment Framework — Authoring Guidance (INTERNAL)

> **Internal planning document — not published to the course site.** The student-facing
> version is the **"Assignments"** page (`docs/assignment-framework.md`, `/assignments/`).
> This file holds the guidance for whoever is *writing* the assignments.

## Why the framework works across our skill range

**Design, spec writing, and test writing are novel to nearly every student regardless of Python
background**, so they level the playing field. Implementation can be scaffolded for students who
need it and delegated to a coding agent by students who don't — *without changing what the exercise
actually assesses.* This is what lets one course serve both the rudimentary and the highly skilled
programmer.

The **design stage** (`course-structure.md` §1) is the strongest version of this: nobody arrives
fluent at decomposing a biological question into computable ones, so cycle 1 starts everyone at
roughly the same place on the thing that matters most.

## Which piece to withhold

Each problem withholds exactly one of the four artifacts. **The strip is the canonical
representation** ([`course-structure.md`](course-structure.md) §5); which piece is withheld varies
for authoring reasons and is not a rotation students track. **Do not use exercise-type letters** —
the student-facing `docs/assignment-framework.md` still describes an A–D scheme and needs rewriting.

| Withheld piece | Seat label | Accountable product |
|---|---|---|
| **CODE** | Implementer | Line annotation + the process record in `notes.md`, including what the agent decided silently. Agent may write the code. |
| **TESTS** | Verifier | **A test without a worked, hand-calculated expected value in its docstring is not accepted** — that is the component an agent cannot produce without the student already understanding the problem. |
| **SPEC** | Reverse engineer | Reimplementable spec + gap analysis. **Grade the gap analysis more heavily than the spec** — finding underspecification shows more than a complete-but-unsurprising spec. |

Every problem is *designed* by the student in the previous cycle, whichever piece is withheld
(`course-structure.md` §1).

## Author rule 1 — problem statements are questions, not tasks

The design stage collapses if the problem statement contains its own decomposition.

| ✅ Genuine question | ❌ Leaks the design |
|---|---|
| "Which of these reads are rRNA, and how confident can you be?" | "Implement a k-mer Naive Bayes classifier." |
| "Do these cells fall into distinct types, and how would you know?" | "Cluster the cells with k-means and pick *k*." |
| "Which genes best separate responders from non-responders?" | "Rank features by random-forest importance." |

**Corollary — over-provide context deliberately.** A good problem statement supplies facts it never
uses, so that the gaps in our materials are discoverable rather than tricks. The archived Week 1
draft mentions `N` bases and lowercase masking without connecting them to anything; that is what
makes the corresponding absences findable. **Trimming a problem statement for length silently breaks
the divergence prompts that depend on it** — they are coupled.

## Author rule 2 — biological grounding

**Every exercise must use a problem whose correct answer is verifiable from domain knowledge
without running any code.** This is what makes the Verifier seat assessable and connects the
framework to biology-first students. It must hold **simultaneously** with rule 1, which is what
makes problem statements the fussiest part of authoring.

- **Good fits** (checkable by hand from biology): FASTA/FASTQ parsing, reverse complement,
  codon translation, GC content, genomic interval overlap, alignment summary stats,
  k-mer / Naive Bayes classification.
- **Poor fits** (require running code to verify): sorting algorithms, abstract data
  structures, string puzzles. **Do not use these.**

## Author rule 3 — plant productive uncertainty

If the provided materials are flawless and obvious, the divergence analysis has nothing to bite on.
*Productive uncertainty* is the working term; it covers four kinds, and a good problem has some of
each:

| Kind | Example |
|---|---|
| **A defensible-but-arguable choice** | Composition-based classification rather than alignment |
| **An unexamined assumption the problem statement quietly contradicts** | Class priors from balanced reference sets, when the real library is 70–90% rRNA |
| **A real defect that does not announce itself** | Empty k-means clusters collapsing silently; `KeyError` on `N` |
| **An absence — something the spec fails to say**, which the student's own agent then decides silently | The spec is silent on lowercase, `N`, and trailing bases; the generated code handles all three anyway |

The **absence** variety is only available when the student authors the code (Implementer), and may
be the strongest form: the undocumented decision is one the student produced themselves, so there is
nobody else to defer to and nothing to take on faith.

**Per-problem checklist:** at least one item most students should find, at least one that rewards
deeper digging (a derivation, a profiling pass, or a real-data check — these become depth-branch
prompts if [`future-depth-branches.md`](future-depth-branches.md) is reintroduced), and **at least
one that a strong design would have caught** — that last is what keeps *"where was your design
better?"* from being a rhetorical question.

### Rule 3b — heavy and light problems

Not every problem carries the full apparatus. Of the eleven problems, **about six are "heavy"**:
full planted-uncertainty inventory (per the checklist above) and deeply-graded divergence analysis.
The rest are **"light"**: one planted item, rubric-graded. The alternation is invisible to students —
every cycle has the same shape from their chair — but it halves the fussiest authoring and
concentrates deep grading where it pays. Heavy slots should include the problems whose divergence
teaches the most: the first classifier (P4), evaluation (P5), and clustering (P11) are obvious
candidates.

### Rule 3a — verify reachability by running it

Whether a planted item is *findable* depends on the fixture, not only on the code. The archived Week
10 draft's empty-cluster defect is unreachable on generic continuous data (200 random seeds produced
none) and requires duplicate or all-zero rows — realistic for scRNA-seq, but only if deliberately
present. **That was discovered by executing the example, not by reading it.**

Every planted item needs a verified note on how it surfaces, or the problem ships with defects
nobody can find and instructor hints that fire every time. Worked inventories with verified numbers:
[`archive/examples-v1/`](archive/examples-v1/).

## Open decisions

The deliverable bundle is fixed: `design.md` · `spec.md` · `test_*.py` · `impl.py` · `notes.md`,
identical every cycle; the process record is a section of `notes.md`
([`course-structure.md`](course-structure.md) §5).

**Still open under [issue #5](https://github.com/bu-bioinfo/bf550/issues/5):** a grading rubric per
starred artifact, a rubric for the divergence analysis, and the toolchain/runtime (Python version,
test runner, provided agent).

## Templates

Authoring templates live in [`internal/templates/`](templates/):

| Template | Use |
|---|---|
| [`assignment-template.md`](templates/assignment-template.md) | TILT problem template. **One file per problem, spanning both cycles** — released in two parts (design cycle, then build cycle). |
| [`checkin-quiz-template.md`](templates/checkin-quiz-template.md) | The **No-AI code-reading** check-in (AIAS 1). |

> **Two different things are called "check-in" and they must not be confused.** The
> code-reading check-in above is a graded No-AI assessment. The **reading check-in that opens each Design session**
> (`course-structure.md` §8) is a low-stakes, near-ungraded prompt whose job is to tell the
> instructor live which part of the reading did not land. **A template for the reading check-in
> does not exist yet** and is needed before the term.
