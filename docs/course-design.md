---
title: "Course Design & Philosophy"
permalink: /design/course-design/
toc: true
toc_sticky: true
---

## What this course is

BF550 is an **applied statistics and machine-learning course for life scientists**. Its
intellectual goal is to give students *intuition for the landscape of ML algorithms* —
how the major classes differ, what problem each is suited to, and how to choose among
them — grounded in real molecular-biology and genomics problems rather than abstract
toy datasets.

It is **not** a from-scratch programming course, and it is not a deep mathematical
theory course. It is a course about **judgment**: choosing the right method, posing the
right problem to a computational tool, and verifying that the answer you get is the
answer you needed.

## The central bet: code *literacy* over code *authorship*

The program requires some programming background, but in practice students arrive across
a wide spectrum — some are rudimentary, some are highly skilled. We have repeatedly
struggled to reliably deliver basic coding instruction to *all* of them in a single
course without either boring the strong students or losing the weak ones.

In the age of generative AI and coding agents, we are making a deliberate, somewhat
controversial choice:

> **The primary coding learning objective is to *read and understand* code — to be code
> *literate* — not to author code from scratch.**

Code literacy here means more than syntax and control flow. It includes:

- **Local comprehension** — reading a snippet and stating precisely what it does, line by
  line, including edge-case behavior.
- **Specification recovery** — inferring the intended contract (inputs, outputs, invariants)
  from an implementation and its tests.
- **Design & organization literacy** — understanding *how code is structured to solve the
  problem at hand*: interfaces, decomposition, data flow, where complexity lives, and
  whether the design fits the larger pipeline.
- **Verification literacy** — knowing how to tell whether code (your own, a colleague's, or
  an agent's) actually does what was intended.

This bet lets us meet students where they are. Specification, testing, and critique are
**novel to nearly everyone regardless of Python background**, so they level the playing
field; implementation can be scaffolded for students who need it and delegated to a
coding agent by students who don't — *without changing what the exercise actually
assesses.*

## Coding agents are assumed, not banned

Students are **provided coding-agent capabilities** and are explicitly expected to use
them. The course is designed so that agent use cannot circumvent the learning goals,
because the graded intellectual product is the part an agent cannot do *for* you:

- **Design and specification** are the student's product — an agent's spec is the agent's
  understanding of the problem, not the student's.
- **Tests with hand-calculated expected values** require the student to already understand
  the problem.
- **Verification and critique** — diagnosing *why* generated code fails, and judging whether
  a design is sound — are the skills we are actually teaching.

The aim is to model what a professional does: constrain the problem first (design → spec →
tests), *then* generate code to satisfy those constraints, then verify. A student who
generates code first and retrofits a rationale has inverted the process and produced
nothing verifiable. See [assignment-framework.md](https://bu-bioinfo.github.io/bf550/design/assignment-framework/).

## Borrowed engineering practices

The assignment scheme deliberately borrows from established software-engineering
disciplines, recast as *thinking tools* rather than as coding mandates:

- **Test-Driven Development (TDD)** — express desired behavior as tests before
  implementation exists.
- **Behavior-Driven Development (BDD)** — describe behavior in terms of observable,
  domain-meaningful outcomes ("given a pure-GC window, the GC fraction is 1.0").
- **Design-Driven Development** — make interface and decomposition decisions explicit and
  reviewable before committing to an implementation.

## Two pedagogical frameworks

The course is built on two named frameworks, applied consistently:

### TILT — Transparency in Learning and Teaching

Every assignment is written in the **Transparent Assignment** structure of
**Purpose / Task / Criteria**:

- **Purpose** — *why* the work matters and which skills/objectives it builds.
- **Task** — *what* the student concretely does, with explicit steps and deliverables.
- **Criteria** — *how* the work is evaluated, with the standard visible in advance.

Transparency is associated with gains in student confidence, belonging, persistence, and
metacognitive awareness — especially valuable given our wide range of incoming skill.
See the [assignment template](https://bu-bioinfo.github.io/bf550/design/templates/assignment-template/).

### AIAS — AI Assessment Scale

Every assessment names a level on the five-point AI Assessment Scale so AI expectations
are unambiguous:

| Level | Name | In this course |
|------:|------|----------------|
| 1 | No AI | Closed-book code-reading (e.g. the written midterm) |
| 2 | AI Planning | Brainstorming/outline help, student develops ideas independently |
| 3 | AI Collaboration | AI drafts/feedback; student critically evaluates & modifies |
| 4 | Full AI | Agent generates code throughout; student directs, annotates, verifies |
| 5 | AI Exploration | Open-ended/creative use, co-designed approaches |

Most labs and coding assignments sit at **Level 4** (full agent use, with the design,
spec, tests, verification, and critique as the student's accountable product). The
code-reading **midterm sits at Level 1**. See
[assessment-and-ai-policy.md](https://bu-bioinfo.github.io/bf550/design/assessment-and-ai-policy/).

## How the pieces fit together

```
Lectures (2×75 min)      → concepts: stats foundations, ML algorithm classes,
                            how to choose a method, how methods are evaluated

Lab (1–2 hr)             → design → spec → test → implementation exercises
                            (4 types, A–D), agent-assisted, biologically grounded

Weekly check-in quiz     → read a provided code snippet, describe what it does
                            (code-literacy practice, low stakes)

Written midterm          → code reading under exam conditions (AIAS Level 1)

Synthesis project        → produce design + spec + tests + implementation for a
                            real method on a real molecular-biology problem
```

> **DECISION:** confirm credit-hour expectations and whether there is a final project
> *and* a final exam, or a project in lieu of a final. Current draft assumes a synthesis
> project rather than a cumulative final exam.