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

- **Final assessment & weights** — *resolved ([#2](https://github.com/bu-bioinfo/bf550/issues/2)).*
  The **synthesis project is the culminating assessment; there is no separate final exam.**
  The 4-credit structure imposes no required assessment minimums. Grade weights confirmed:
  labs 35% / check-in quizzes 10% / midterm 20% / synthesis project 30% / participation 5%.

> Other open decisions live in the relevant internal docs and in the
> [discussion issues](https://github.com/bu-bioinfo/bf550/issues).
