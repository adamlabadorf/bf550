---
title: "How This Course Works"
permalink: /about/
toc: true
toc_sticky: true
---

BF550 is an applied statistics and machine-learning course for life scientists. The goal is
to build your **intuition for how machine-learning methods work and when to use them**, and
to apply that intuition to real molecular-biology and genomics problems. This page explains
how the course is structured and what to expect.

## What you'll learn

You'll come away able to:

- Recognize the major **classes of machine-learning algorithms** — supervised vs.
  unsupervised, classification, clustering, feature-importance and tree-based methods,
  dimensionality reduction — and understand how they differ.
- **Choose the right method** for a given biological question and dataset, and explain why.
- **Read and understand code**: say precisely what a piece of code does, recover the idea
  behind it, and judge whether it's well designed for the problem.
- **Work effectively with AI coding agents** — break a problem down, direct an agent to
  build a solution, and verify that the result actually does what you intended.

The emphasis throughout is on *judgment*: framing the problem, picking the method, and
checking the answer.

## Reading code is the focus

You come into this program from many different starting points — some of you have written a
lot of code, some very little. **This course focuses on reading and understanding code, not
on writing it from scratch**, so wherever you start, you'll be building the same core skill:
*code literacy*.

Code literacy is more than syntax. It means being able to:

- read a snippet and explain exactly what it does, including the tricky edge cases;
- look at code plus its tests and reconstruct the specification it was built to meet;
- see how a program is organized to solve a problem, and where its complexity and risk live;
- tell whether a piece of code — yours, a classmate's, or an AI's — actually works as
  intended.

These are the skills that make you effective with any codebase, and they're exactly the
skills you need to use AI coding tools well.

## Using AI coding agents

You'll be **provided with coding-agent tools, and you're encouraged to use them.** This
course is built around them rather than against them.

The work you turn in is structured so that the agent handles what it's good at (generating
code) while *you* do the thinking that matters: defining the problem, specifying what a
correct solution looks like, writing tests, and verifying the result. In practice that means
working the way professional engineers do — **constrain the problem first (design →
specification → tests), then generate the code, then check it against what you specified.**

Each assignment tells you exactly what level of AI use is expected (see
[AI levels](#two-things-youll-see-on-every-assignment) below), so there's never any
ambiguity about what's allowed.

## How the course fits together

| Component | What you do |
|---|---|
| **Lectures** (2 × 75 min/week) | Build the concepts: statistics foundations, the classes of ML algorithms, how to choose a method, and how methods are evaluated. |
| **Lab** (1–2 hr/week) | Hands-on exercises using the **design → spec → test → implementation** framework, agent-assisted and grounded in a real biological problem. |
| **Weekly check-in quizzes** | Short code-reading practice: you're given a snippet and describe what it does. |
| **Written midterm** | Code reading under exam conditions (no AI). |
| **Synthesis project** | Bring it all together: design, specify, test, and build a real method for a real molecular-biology problem. |

Labs use a framework where each exercise gives you some pieces of a problem and asks you to
produce the missing one — sometimes you write the tests, sometimes you recover the
specification, sometimes you critique an implementation. See the
[assignment framework](https://bu-bioinfo.github.io/bf550/assignments/) for
details.

## Two things you'll see on every assignment

**Clear expectations (Purpose / Task / Criteria).** Every assignment states up front *why*
you're doing it, *what* exactly to do, and *how* it will be evaluated — so you always know
what success looks like before you start. (This follows the
[TILT](https://www.tilthighered.com/resources) transparent-assignment framework.)

**An AI use level.** Every assignment is labeled with a level on the
[AI Assessment Scale (AIAS)](https://aiassessmentscale.com/), telling you how much AI use is
expected:

| Level | Name | What it means |
|------:|------|---------------|
| 1 | No AI | Work on your own (e.g. the code-reading check-ins and midterm). |
| 2 | AI Planning | AI for brainstorming/outlining; you develop the ideas yourself. |
| 3 | AI Collaboration | AI helps draft; you critically evaluate and revise its output. |
| 4 | Full AI | Use the agent throughout; you direct it, verify it, and own the result. |
| 5 | AI Exploration | Open-ended, creative use. |

Most labs and the project are **Level 4** — use the agent freely, with your design,
specifications, tests, and verification as the work that's graded. The code-reading
check-ins and midterm are **Level 1**, so you and we can both see your unaided reading skills
grow over the term.
