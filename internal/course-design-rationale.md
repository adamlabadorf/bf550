# Course Design Rationale (INTERNAL)

> **Internal planning document — not published to the course site.** This captures the
> *why* behind BF550's design for the instructor team. The student-facing version of this
> material is the **"How This Course Works"** page (`docs/course-design.md`,
> `/about/` on the site), which is written to address students directly and omits the
> rationale and open decisions below.

## What this course is (and isn't)

The intellectual goal is to give students *intuition for the landscape of ML algorithms* —
how the major classes differ, what each is suited to, and how to choose among them —
grounded in real molecular-biology problems rather than toy datasets.

It is deliberately **not** a from-scratch programming course and **not** a deep
mathematical-theory course. The organizing principle is *judgment*: choosing the right
method, posing the right problem to a computational tool, and verifying the result.

## The central bet: code literacy over code authorship

The program requires some programming background, but in practice students arrive across a
wide spectrum — some rudimentary, some highly skilled. We have repeatedly struggled to
reliably deliver basic coding instruction to *all* of them in a single course without
either boring the strong students or losing the weak ones.

In the age of generative AI and coding agents, we are making a deliberate, somewhat
controversial choice: **the primary coding learning objective is to *read and understand*
code — to be code literate — not to author code from scratch.**

Why this works pedagogically:

- Specification, testing, and critique are **novel to nearly everyone regardless of Python
  background**, so they level the playing field.
- Implementation can be scaffolded for students who need it and delegated to a coding agent
  by students who don't — **without changing what the exercise actually assesses.**

**The bet now has mainstream backing — and one sharp empirical caveat.** The computing-education
field has converged on the same position: Denny et al. (2024, *CACM* 67(2)) and the ACM Task Force
on Generative AI and Programming Assessment (2026, surveying 750+ educators) both recommend
shifting emphasis toward code comprehension, design, testing, and critical evaluation of
AI-generated output, with secured no-AI assessment alongside open-AI work. The caveat is Prather
et al. (2024, ICER), who show GenAI *compounds* struggling novices' metacognitive difficulties and
leaves them with an **illusion of competence** while capable students accelerate — a widening gap.
The course's countermeasures (No-AI check-ins, the sealed design stage, hand-calculated test
values, the divergence analysis) exist precisely to close that gap; **per-student check-in
trajectories are the early-warning instrument** and should be watched, since class averages will
hide it. Full citations and analysis:
[`computational-thinking-basis.md`](computational-thinking-basis.md) §4.

## Why agents are assumed, not banned

Students are provided coding-agent capabilities and expected to use them. The design ensures
agent use cannot circumvent the learning goals because the graded product is the part an
agent cannot supply: the design, the specification, the hand-calculated tests, the failure
log, and the critique. A student who generates code first and retrofits a rationale has
inverted the process and produced nothing verifiable. The structure forces "constrain first
(design → spec → tests), then generate, then verify."

## Pedagogical frameworks (rationale)

- **TILT** — transparent assignments (Purpose/Task/Criteria) are associated with gains in
  student confidence, belonging, persistence, and metacognitive awareness — especially
  valuable given our wide range of incoming skill.
- **AIAS** — labeling each assessment's AI level removes ambiguity and lets us be
  agent-positive without compromising the No-AI baseline (check-ins, midterm) that
  triangulates each student's unaided code literacy.

## Resolved decisions

- **Final assessment & weights** — the **synthesis project is the culminating assessment; there
  is no exam in finals period.** Two secured in-class exams close the course's two act
  boundaries: the midterm (cycle 8, Acts I–II) and the **Act III exam** (cycle 13's Design
  session, cycles 9–11) — added because the re-sequenced calendar concentrates the most judgment-heavy,
  least-verifiable material after the midterm, and it would otherwise carry no secured
  assessment. Weights: **problems 30 / check-ins 10 / midterm 15 / Act III exam 15 / project 30
  / participation 5** (supersedes the weights in [#2](https://github.com/bu-bioinfo/bf550/issues/2);
  the project stays at 30% so the incentive structure and the stated philosophy agree). The
  4-credit structure imposes no required assessment minimums.

> Other open decisions live in the relevant internal docs and in the
> [discussion issues](https://github.com/bu-bioinfo/bf550/issues).
