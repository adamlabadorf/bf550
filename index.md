---
link-citations: true
---

> **UNDER CONSTRUCTION.** This site is being bootstrapped. Content, schedule, and
> policies are drafts — see the planning docs in the
> [GitHub repository](https://github.com/bu-bioinfo/bf550) and the open
> [discussion issues](https://github.com/bu-bioinfo/bf550/issues).

**Semester:** Fall (this year) · **Meeting time:** Mon/Wed/Fri, 105 minutes each _(times TBD)_ · **Location:** _TBD_

**Prerequisites:** some prior programming experience (any language) and introductory molecular
biology. A wide range of programming and math backgrounds is expected — the course is designed
for it, as you're about to read.

## Why this course is built the way it is

Two things are true at once. Machine learning has become the working language of modern
biology — and AI can now write competent code from a plain-English description. Some courses
respond to that second fact by banning AI. We do the opposite: **we assume it, provide it, and
build the course around the skills it cannot do for you.**

Here is what an AI cannot do for you. It cannot decide what question your data can actually
answer. It cannot decide what "correct" means for a problem you care about. It cannot tell you
whether the confident-looking answer it just produced is wrong. Those three skills — framing a
problem, defining correctness, and catching failure — are what this course teaches, using
machine learning on real biological data as the material.

You will read far more code than you write. That is deliberate. You come into this program with
wildly different programming backgrounds, and we are not going to pretend otherwise. Reading
code — saying precisely what it does, recovering what it was *meant* to do, judging whether it
should be trusted — is a skill almost none of you have practiced, regardless of background. It
levels the field, and in the age of AI-generated code, it is *the* skill.

The same goes for math. Some of you have a lot; some very little. Every idea in this course
arrives in the same order: first as a **story** about how data comes to exist, then as **code**
you can run and poke, and only then as **notation** — the formula, presented as a compressed
summary of something you have already played with. If you can read Python, you can learn to
read math. Formulas are never the entrance fee here; they are the souvenir.

## The weekly rhythm

Every problem in this course lives for two weeks, and you work on it twice.

**Week one: you design.** You get a biological question — a real one, like *"which of these
sequencing reads are ribosomal RNA, and how confident can you be about any single call?"* — and
nothing else. No starter code, no instructions. Over the week, you write down your approach:
What process produced this data? What would have to be computed or estimated? What would the
right method need to be able to do? And — the question that separates scientists from
software — *how would your approach lie to you?* You commit your design by Sunday night. It is
graded only for being on time. **Being wrong in a design is not just acceptable, it is the
point**, and you will see why on Wednesday.

**Week two: you compare and build.** Our materials for that problem unseal: a specification, a
test suite, and an implementation — minus one piece, which is yours to produce. Before you
build anything, you write a short **divergence analysis**: where did our approach differ from
the one you committed to? What did we handle that you didn't think of? And — a question we mean
sincerely — *where was your design better than ours?* Our materials are written by people with
opinions and deadlines. Some weeks they contain choices you should argue with. Occasionally
they contain a genuine mistake. Finding those earns credit. Deferring to us because we're the
instructors earns nothing.

Which piece we withhold varies, and the assignment header always shows it:

```
Design week      DESIGN      SPEC      TESTS      CODE
                ★ YOURS    ▨ sealed  ▨ sealed   ▨ sealed

Build week       DESIGN      SPEC      TESTS      CODE
              (committed)    given     given    ★ YOURS
```

Where the star lands, you have a seat: **Implementer** (make it work, and be able to explain
every line), **Verifier** (prove it works, with expected values you calculated by hand), or
**Reverse engineer** (recover the specification nobody wrote down, and find what the tests fail
to pin down).

**The week itself runs Monday/Wednesday/Friday, 105 minutes each.** Monday: a short check-in on
the reading, then we work with the ideas you read about — this course is flipped, and the
textbook is where you meet material first. Wednesday: studio — materials unseal, you compare
and build, with instructors and TAs in the room. Friday: we break things. We take the method
you just built and make it fail — violated assumptions, leaked data, overconfident scores —
because knowing *how a method lies* is the difference between using it and being used by it.
Fridays are also where designs and discoveries get compared across the room.

The week-by-week topics and problems are on the [schedule]({{ site.baseurl }}/schedule/).

## Using AI

You'll have a provided coding agent and a textbook tutor, and every assignment states its
[AI level](https://aiassessmentscale.com/) plainly:

- **Design weeks — AI for brainstorming only.** The design must be your thinking. This is the
  one place the course asks you to work mostly unaided, because it is the one skill that dies
  if you delegate it.
- **Build weeks — full AI, encouraged.** Let the agent write code. What we grade is what agents
  can't fake: your hand-calculated values, your annotations, your account of what the agent
  silently decided on your behalf.
- **Check-ins and the midterm — no AI.** Short code-reading exercises, every other week,
  closed-book. These exist for your benefit as much as ours: research on novices using AI finds
  that the students who struggle most are often the ones most convinced they're doing fine. The
  check-ins are how you and we both see your *unaided* skill actually growing — so nobody
  discovers a gap for the first time during the midterm.

## Going deeper, your way

Six times during the term (your choice of weeks, at least one from each), you'll add a
**depth section** to your build-week write-up:

- **Math** — derive why the estimator is what it is
- **Compute** — make it fast, robust, or scalable
- **Bio** — find the assumption real data violates, and what it costs

These are *different directions*, not different difficulty levels. The Friday sessions where
depth work gets shared exist so that the room ends up knowing what each direction found. Pick
by curiosity, not by what sounds impressive.

## What you hand in, and what it's worth

Every problem, the same shape: your committed `design.md`, the artifact your seat produces,
and one `notes.md` holding your divergence analysis, your annotations or analysis, and (six
times a term) your depth section.

| | Weight | AI level |
|---|---:|---|
| Weekly problems (designs + builds) | 35% | Design: planning only · Build: full |
| Check-in quizzes (biweekly, code reading) | 10% | None |
| Written midterm | 20% | None |
| Synthesis project | 30% | Full, with your design as the spine |
| Participation (Fridays count) | 5% | — |

The synthesis project is the course in miniature and there is **no final exam**: a complete
design → specification → tests → implementation for a real method on a real biological problem,
every decision defended. By then you'll have done the design move a dozen times. It will feel
like the most natural thing in the world.

**If you miss a week** — it happens — the design converts to a hindsight-critique variant with
the same credit, and you rejoin the pipeline the following Monday. One missed week costs one
week, never more. Ask early.
