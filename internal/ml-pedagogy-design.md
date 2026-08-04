# ML Pedagogy Design — Probabilistic Frame & MWF Format (INTERNAL)

> **Internal design document — not published to the course site** (`internal/` is excluded in
> `_config.yml`). This records the design discussion behind how BF550 presents its machine
> learning content: the probabilistic framing, how it is delivered across three 105-minute
> MWF sessions, and how the course serves a wide range of incoming mathematical background.
>
> Companion docs: [`course-design-rationale.md`](course-design-rationale.md) (the *why* of the
> course overall), [`assignment-framework-authoring.md`](assignment-framework-authoring.md)
> (how to write the labs), [`open-decisions.md`](open-decisions.md) (what is still unsettled).
>
> **Status: agreed direction, not yet propagated to student-facing pages.** See
> [Pending propagation](#pending-propagation-to-student-facing-pages) at the end.

---

## 1. The problem this design solves

Students arrive with mathematical backgrounds spanning from very little to a great deal. The
course needs to be **challenging across that whole range without anyone feeling left behind.**
This is the same problem the course already solves for *programming* background via the
code-literacy bet; this document is the equivalent solution for *mathematical* background.

We want a **probabilistic frame** for the ML content — it is the frame that makes the methods
cohere rather than appearing as a bag of tricks — without that frame becoming a mathematical
gate at the door.

### The two reference texts, and what we take from each

| Text | What we take | What we leave |
|---|---|---|
| **Bishop, *Pattern Recognition and Machine Learning*** | The *organizing frame*: methods as probability models; generative vs. discriminative; regularization as a prior; mixtures; latent-variable views | The derivations, the notation density, the assumed calculus/linear algebra |
| **McElreath, *Statistical Rethinking*** | The *delivery method*: minimal notation, intuition first, simulation as the explanatory device, models as stories | The full-Bayesian inference machinery (MCMC/Stan) — see [deferred fork 1](#5-deferred-forks) |

## 2. The key observation about McElreath's method

It is worth being precise about *why* Statistical Rethinking works for readers with modest
math, because the reason is not simply "less math":

> **Simulation replaces derivation as the primary explanatory device.** You state the model as
> a generative story, write the handful of lines that produce fake data from it, then ask what
> could have produced the data you actually observed. Probability becomes counting and running
> things before it becomes algebra.

This fits BF550 unusually well, because **the course's medium is already code.** A generative
story *is* code. So "read the model" and "read the code" become the same act, and the
probabilistic frame reinforces the central code-literacy bet rather than competing with it for
time.

## 3. Core commitments

### 3.1 Notation literacy *is* code literacy

The course already argues that reading a compressed formal description and saying what it does
is the skill that matters. **We apply that claim verbatim to mathematical notation.** Notation
is not a prerequisite to be gated on; it is a second notation system to become literate in,
taught the way we teach Python — by reading it, not by manipulating it.

This is the single reframe that makes the rest of the design hang together, and it is worth
stating to students explicitly.

### 3.2 The story → code → notation convention

**One public convention we never break: every idea arrives as a story, then as code, then as
notation — in that order.** The formula appears at the *end* of a topic, as the compression of
something students have already simulated and perturbed.

Two payoffs, one for each end of the range:

- **Students with little math** stop experiencing formulas as the gate. By the time
  `p̂ᵢ = (nᵢ + α) / (N + αK)` appears, they have already added pseudocounts in a loop and
  watched the estimate drift toward uniform.
- **Students with a lot of math are not bored**, because *reading and critiquing* a formal
  statement — "what does this expression assume? where does it break?" — is a genuinely
  different skill from deriving it, and most of them have not practiced it.

> **Author rule.** No formula is presented before the simulation it summarizes. If a lecture
> draft leads with notation, it is not finished. `_lectures/week-03.md` currently leads with
> the Laplace-smoothing formula and needs reordering under this rule.

### 3.3 The notation decoder

A single **growing "notation decoder" page**, referenced all term, accumulating symbols as they
appear with a plain-language and a code gloss for each.

**We do not publish a math-prerequisites announcement.** Naming prerequisites sorts students
into "qualified" and "not" before the course starts; an always-available decoder does the same
work without the sorting.

### 3.4 Hard design constraints

Two constraints to hold throughout, because they are what make "no one left behind" real
rather than aspirational:

1. **The core path of every lab is completable without calculus.**
2. **No formula is presented cold** (see 3.2).

## 4. Weekly format: 3 × 105 minutes, MWF

Rather than framing this as "one lecture plus two labs," each session gets a distinct **verb**.
The three verbs are the probabilistic modeling workflow itself — which is why the format and
the pedagogy reinforce each other:

| Day | Session | Shape | What it is |
|---|---|---|---|
| **M** | **Build the model** | ~25–30 min exposition + live simulation → paired predict/run/explain → ~15 min naming the notation | The generative story for this week's method, arrived at by simulating it |
| **W** | **Build the code** | Full studio | The week's lab on the biological anchor, agent-assisted |
| **F** | **Break the model** | Critique clinic + depth share-out | Where it fails: overfitting, leakage, violated assumptions, uncalibrated output |

### Why Friday is worth protecting

Friday is the session most at risk of being reclaimed for content, and the one to guard hardest:

- It is where the schedule's *"a recurring theme, not a one-time topic"* commitment gets teeth.
  Every method offers a fresh way to get generalization wrong; a standing session means that
  recurrence does not have to be scheduled topic by topic.
- It is the natural home for the reviewer- and analyst-seat exercises (§6).
- It is where **depth branches get shared out** (§7), which is what keeps differentiated depth
  from siloing.

### Format note: this is effectively a studio course

At 315 minutes/week of contact, the bulk of student effort lands *in the room*. Out-of-class
reading should stay genuinely modest — a Rethinking chapter is readable in an evening in a way
a PRML chapter is not. Budget out-of-class time for reading plus finishing the Wednesday lab,
and no more.

## 5. One template, ten times

Every method is introduced with the same four slots. This doubles as a rubric structure, a
check-in quiz format, and a one-page **model card** students fill in each week:

1. **The story** — what process would generate data like this? (in prose *and* in ~10 lines of code)
2. **What's unknown** — which parts of the story are parameters?
3. **How we pin them down** — counting, optimizing a loss, or a posterior
4. **How it lies to you** — assumptions violated, failure modes, what a fooled version looks like

By Week 13 students hold ten of these side by side, and that stack **is** the "intuition for the
landscape of ML algorithms" learning objective, made physical. It is also the obvious scaffold
for the synthesis project.

## 6. Probabilistic reframes, week by week

Most of the existing schedule survives intact. These are the weeks where the probabilistic
frame changes the content materially, highest value first:

| Wk | Current topic | Reframe | Why it earns its place |
|---:|---|---|---|
| 10–11 | Clustering | **k-means as the hard-assignment limit of a Gaussian mixture** | GMM is what makes k-means make *sense* (why spherical? why does it fail on elongated clusters?). EM's intuition — guess assignments, update parameters, repeat — needs zero calculus. Biggest single upgrade available. |
| 4 → 6 | Naive Bayes → logistic regression | **The generative/discriminative pivot**, taught back to back | Naive Bayes literally generates a read from a class; logistic regression models `p(y\|x)` directly. Same problem, two philosophies. PRML 4.1–4.3; the best conceptual moment in the course. |
| 3 | Probability for ML | Add **grid approximation** (Rethinking ch. 2) | Highest-leverage single technique for this audience: a posterior becomes a `for` loop over candidate parameter values, no calculus, and the prior→posterior update is *watchable*. Five lines of readable code unlock the word "posterior" for the term. |
| 12 | Regression & regularization | **Regularization is a prior** — ridge = Gaussian, lasso = Laplace | Closes a loop Week 3 already opens ("add a pseudocount *is* assume a mild prior"). Third appearance of one idea. |
| 5 | Evaluation | A classifier emits a **distribution**; thresholding is a separate decision-theoretic step (PRML 1.5) | Earns **calibration**, usually skipped, and exactly the right criticism of variant-pathogenicity scores. |
| 9 | Dimensionality reduction | **Probabilistic PCA as the intuition** (latent-variable story), even if computed via SVD | Makes PCA a model with assumptions rather than a rotation recipe. |
| 7 | Trees & forests | The **honest outlier**: what you gain and lose when you drop the probability model | Naming the exception strengthens the frame instead of hiding a gap. Loses calibrated uncertainty; gains interpretability and non-linearity for free. |
| 13 | Neural nets | The same likelihood machinery, stacked | Continuity rather than novelty. |

### The through-line worth naming: uncertainty

The probabilistic frame buys students something specifically biological. In genomics,
essentially every quantity is a noisy estimate from a small sample. The difference between a
student who reports *"my classifier got 0.91 AUC"* and one who reports *"here is the
distribution of AUCs across resamples, and here is why I don't trust the point estimate"* is
the clearest single measure of whether this design worked.

## 7. Depth branches: challenge without tiers

The usual approach to a wide range — optional harder problems — quietly brands a second tier
and mostly rewards students who were already comfortable. Instead:

**Every lab has one core path everyone completes, plus three optional branches that are
different *kinds* of depth rather than different amounts.**

| Branch | Prompt |
|---|---|
| **Math** | Derive why the estimator for this model is what it is |
| **Compute** | Make it robust or fast — log-space to avoid underflow, vectorize, scale it up |
| **Bio** | Which assumption does real data violate, and what does that cost you? |

Why this works where tiering does not:

- Students **do not sort cleanly by math background.** CS-strong students take the compute
  branch; wet-lab students take the bio branch. There is no single ladder to be low on.
- **Friday's share-out pushes each branch back into common knowledge**, so depth is
  redistributed rather than siloed — and each student is the person who knows something the
  others need.

**Author rule: every branch must be genuinely useful to the others.** A branch nobody else
needs to hear about is a bonus problem wearing a costume.

**The three branch names stay fixed all term** — one choice from a stable menu, never a new
structure to learn (see §8.4).

## 8. Exercise-type legibility

The four exercise types (A–D) risk being hard for students to follow. The diagnosis below and
the four fixes are the response.

### 8.1 Diagnosis: it is not "four types," it is five simultaneous axes

Four types is not itself much to hold. The load comes from what a student must track at once:
**which type, which deliverables, which AI level, which biological anchor, which depth
branch.** Three specific aggravating factors:

1. **Letter names are opaque.** "Type C" carries no meaning; the student must maintain a
   memorized mapping from letter → pieces given → thing to produce. This is pure extraneous
   load — it teaches nothing.
2. **The deliverable bundle changes shape every type.** Annotation + failure log for A; four
   distinct kinds of test for B; spec + gap analysis for C; three-level critique + summary
   table for D. That is roughly fifteen distinct requirement types across the term, and per
   [issue #5](https://github.com/bu-bioinfo/bf550/issues/5) the bundle is not yet defined.
3. **Nothing is stable week to week.** Even with TILT stating Purpose/Task/Criteria each time,
   the student re-derives the shape of the work at every lab.

### 8.2 Fix 1 — Show the picture, drop the letter

The four types are not four things. They are **one thing with a moving hole**: the same four
artifacts, with different pieces withheld. Make that visible and there is nothing to memorize.

Every lab header carries the same strip, with the student's piece starred:

```
DESIGN  →   SPEC   →  TESTS   →   CODE
given      given      given      ★ YOURS
```

The student never learns "Type A" — they look at where the star is. **Letters survive as
author-side shorthand only** (in `internal/`, rubrics, and the schedule table), never as the
primary student-facing label.

### 8.3 Fix 2 — Name the seat, not the letter

Pair the strip with a role name. These are real jobs on a real software team, and students
already understand rotating roles from lab work:

| Type | Seat | One-line student framing |
|:--:|---|---|
| A | **Implementer** | "You have the spec and the tests. Make it work — and be able to explain every line." |
| B | **Verifier** | "It claims to work. Prove it, with numbers you worked out yourself." |
| C | **Reverse engineer** | "Here is code nobody documented. What is it *supposed* to do, and what did they forget to pin down?" |
| D | **Reviewer** | "It works. Should it ship?" |

"This week you're the reverse engineer" is memorable in a way "Type C" will never be, and it
carries the professional point the framework is actually making.

### 8.4 Fix 3 — One bundle, always the same files

Replace per-type deliverable bundles with **a single lab repo layout that never changes.** The
seat determines which files arrive pre-filled and which the student writes:

| File | Role | Varies by seat? |
|---|---|---|
| `design.md`, `spec.md`, `test_*.py`, `impl.py` | The four artifacts | Which are given vs. authored |
| `notes.md` | The reflective product — line annotation, gap analysis, or critique, depending on the seat | Content varies; the file does not |
| `log.md` | Process record — the failure log and what it taught you | No |

"What do I hand in?" then has **one answer all term**: the repo, with the starred artifact
filled in, `notes.md` written, and `log.md` kept. The *content* varies; the *shape of
submission* never does.

Depth branches live as **one extra section in `notes.md` titled "Depth"** — pick one of the
three fixed branches, one paragraph plus whatever artifact it produced. This keeps
differentiation entirely outside the required bundle: it adds a choice, not a structure.

This is a concrete answer to issue #5, and it is worth noting it resolves that issue in the
direction of *reducing* load rather than specifying more.

### 8.5 Fix 4 — Cap the requirement count per lab

The Verifier seat (Type B) currently asks for four distinct kinds of test: hand-calculated
example, synthetic, property-based, and documented expected failure. **Property-based testing
is genuinely advanced** — for a student with little programming background that is a cliff, and
it is exactly the population the framework is supposed to protect.

Recommended: **hand-calculated example tests are the required core** (they are the irreplaceable
part — the component an agent cannot produce without the student already understanding the
problem). Synthetic, property-based, and documented-failure tests become **two-of-three
required, with all three as the compute depth branch.** Same ceiling for strong students, a
reachable floor for everyone.

### 8.6 Withdrawn: the fifth exercise type

An earlier proposal in this discussion was a fifth type — **story ↔ code**: given a generative
story in prose, identify which of three implementations matches it, or the reverse. It is the
literacy skill the probabilistic frame is built on, and it is math-background-neutral.

**It should not be a lab type.** Adding a fifth seat cuts directly against everything in §8.

Instead, **story ↔ code becomes a check-in quiz format.** Check-ins are already short, No-AI,
and structurally simple — they have no deliverable bundle, so a new format there costs nothing.
Check-ins then alternate between reading a snippet and reading a story/formula, which broadens
the No-AI baseline from code literacy to formal literacy generally. The probabilistic-literacy
goal lands without touching the lab framework at all.

## 9. Deferred forks

Recorded here, deliberately **not decided** (see [`open-decisions.md`](open-decisions.md)):

1. **How Bayesian?** Recommended leaning: borrow McElreath's *pedagogy and generative framing*
   but not his *inference machinery* — stay at MLE/MAP plus simulation-based uncertainty
   (bootstrap, permutation, resampling), which delivers distributional thinking without
   spending two weeks on MCMC. Grid approximation covers the genuine-posterior cases; full
   Bayes becomes a depth branch, not a unit.
2. **Is the MWF split 1 concept + 2 hands-on, or 2 + 1?** i.e. should Friday also be studio
   time, with critique folded into Wednesday? Recommended leaning: keep Friday distinct — the
   share-out needs its own room — at the cost of one studio session.
3. **Fifth exercise type, or a modifier?** *Partially resolved in §8.6:* story ↔ code moves to
   the check-in quizzes rather than becoming either. Revisit only if check-ins prove too small
   to carry it.

## 10. Pending propagation to student-facing pages

None of the following has been changed yet; recorded so it is not lost.

| What | Where | Note |
|---|---|---|
| **Contact format** is stated as 2 × 75-min lectures + 1 × 1–2 hr lab | `README.md`, `docs/course-design.md`, `docs/schedule.md`, `docs/syllabus.md` | Now **3 × 105-min MWF sessions**; needs updating everywhere it appears |
| **Build / code / break** weekly rhythm | `docs/schedule.md`, `docs/course-design.md` | Replaces the lecture/lab table framing |
| **Seats + the four-box strip** replace letter names | `docs/assignment-framework.md`, `_labs/`, `docs/schedule.md` | Letters stay as author shorthand in `internal/` |
| **One-bundle file layout** | `docs/assignment-framework.md`, [issue #5](https://github.com/bu-bioinfo/bf550/issues/5) | Also resolves the per-type-bundle gap |
| **Depth branches** | `docs/assignment-framework.md`, `_labs/lab-overview.md` | Plus the "must be useful to others" author rule in `assignment-framework-authoring.md` |
| **Notation decoder** page | new page under `docs/` or `_guides/` | Grows through the term |
| **story → code → notation** rule | `internal/` author guidance | Week 3 lecture currently violates it |
| **Verifier test requirements** relaxed to 2-of-3 + core | `docs/assignment-framework.md` | Per §8.5 |
| **Check-in quizzes** alternate code-reading and story/formula-reading | `docs/assessment-and-ai-policy.md`, `internal/templates/checkin-quiz-template.md` | Per §8.6 |
