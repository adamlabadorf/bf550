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
| **M** | **Build the model** | ~25–30 min exposition + live simulation → paired predict/run/explain → ~15 min naming the notation → **the lab's design phase, committed before leaving** | The generative story for this week's method, arrived at by simulating it — then the design of the computation (§8.4) |
| **W** | **Build the code** | Full studio; lab materials unseal here | The week's lab on the biological anchor, agent-assisted |
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

> **This template is also the lab design-phase artifact.** The four slots constitute a design
> document for a probabilistic method, so the card students commit at the end of Monday (§8.4)
> and the card that accumulates into the term-long stack are the same object. One artifact, two
> jobs — and it means the design phase never starts from a blank page.

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
| **Compute** | Make it robust or fast — log-space to avoid underflow, vectorize, scale it up. Also the standing home for the efficiency and composability critique inherited from the old Type D (§8.4): does it do unnecessary work, and would it fit into a larger pipeline? |
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
structure to learn (see §8.5).

## 8. Exercise-type legibility

The four exercise types (A–D) risk being hard for students to follow. The diagnosis below and
the four fixes are the response.

### 8.1 Diagnosis: it is not "four types," it is five simultaneous axes

Four types is not itself much to hold. The load comes from what a student must track at once:
**which type, which deliverables, which AI level, which biological anchor, which depth
branch.** Three specific aggravating factors:

> **Net effect of the fixes below.** The framework ends up as **three seats plus one fixed
> opening phase** (§8.4) rather than four rotating types — fewer moving parts than we started
> with, and every lab has the same first 30 minutes regardless of seat.

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

The seats are not separate things. They are **one thing with a moving hole**: the same four
artifacts, with different pieces withheld. Make that visible and there is nothing to memorize.

Every lab header carries the same strip. **DESIGN is always the student's** (the universal
opening phase, §8.4) and is sealed off from the rest until committed; the remaining boxes are
given-or-starred according to the seat:

```
Phase 1     DESIGN      SPEC      TESTS      CODE
           ★ YOURS    ▨ sealed  ▨ sealed   ▨ sealed

Phase 2     DESIGN      SPEC      TESTS      CODE       ← early term (one hole)
          (committed)   given     given    ★ YOURS

Phase 2     DESIGN      SPEC      TESTS      CODE       ← late term (multi-hole studio)
          (committed)  ★ YOURS   ★ YOURS   ★ YOURS
```

The student never learns "Type A" — they look at where the stars are. **Letters survive as
author-side shorthand only** (in `internal/`, rubrics, and the schedule table), never as the
primary student-facing label.

The strip is also what carries the term-long progression (§8.4) without anyone having to
announce a new structure: the seats are training wheels, and coming off is just more stars.

### 8.3 Fix 2 — Name the seat, not the letter

Pair the strip with a role name. These are real jobs on a real software team, and students
already understand rotating roles from lab work. **Three seats**, all of them phase-2 postures:

| Type | Seat | One-line student framing |
|:--:|---|---|
| A | **Implementer** | "You have the spec and the tests. Make it work — and be able to explain every line." |
| B | **Verifier** | "It claims to work. Prove it, with numbers you worked out yourself." |
| C | **Reverse engineer** | "Here is code nobody documented. What is it *supposed* to do, and what did they forget to pin down?" |

"This week you're the reverse engineer" is memorable in a way "Type C" will never be, and it
carries the professional point the framework is actually making.

There is no fourth seat: **design became the universal opening phase instead** (§8.4). Late in
the term the seats blur deliberately — a studio session may put stars on two or three boxes at
once — so the seat names are a scaffold for the early weeks, not a permanent taxonomy.

### 8.4 The design phase — universal, upstream of every seat

**Every lab opens with the same design phase, before any materials are revealed.** Students
receive only the domain problem, work it down to computable questions and candidate methods,
commit that, and *then* meet the pregenerated materials with their seat's hole in them. The
comparison between the two is the pedagogical engine of the lab.

This supersedes the earlier proposal to make design a fourth *seat* (originally "Reviewer,"
then "Designer"). The seat version was worse, and specifically so:

- **Design would have been the least-practiced skill in the course** — 2–4 encounters in
  thirteen weeks, for the highest-transfer thing we teach. As a universal phase it is practiced
  twelve times.
- **The seat version needed a bespoke two-phase commitment gate that no other seat had.** Making
  phase 1 universal turns that special case into the standard lab rhythm, so anchoring is
  handled structurally rather than by exception.
- **It leaves three seats instead of four.** Three postures plus one fixed opening is less to
  hold than four rotating types — this is a *reduction* against the §8.1 diagnosis, not a new
  axis.

#### Alignment with the computational-thinking instrument

This mirrors pedagogical instruments being deployed in other courses in the program, whose arc
is: **start from a problem statement → break it into solvable components → define the components
as computable questions → select appropriate methods → implement.** Meeting the same
decomposition in several courses is how it becomes a habit rather than a course-specific ritual.

> **DEPENDENCY — vocabulary alignment.** If the instrument has named steps, BF550 must use
> *those names*, not a parallel set invented here. Most of the cross-course value dies if the
> same four moves are called something different in this course. The phase-1 template below uses
> placeholder language until the instrument's step names are confirmed.

#### Why the comparison matters more than the design

The point is not that students produce a good design on the first try. It is that **the
pregenerated materials become evidence rather than authority.** A student who has already
committed to a view reads them critically; a student who opens them cold reads them receptively
and mistakes that for learning. That difference is the whole argument for the sealed phase.

It also catches the failure mode that matters most in computational biology: **code that passes
its tests and faithfully implements its spec, where the spec answered the wrong question.** No
amount of correctness review finds that. An independently-formed set of objectives does.

#### Structure

- **Phase 1 — the problem only.** No spec, tests, or code. Decompose the domain question, state
  what should be computed, what would count as correct, and which failure modes you would worry
  about. Then **commit it.**
- **Phase 2 — materials revealed, seat applies.** Where do the materials' implicit objectives
  differ from yours? Which of your worries did they handle, which did they miss, and which did
  they handle that you never considered? Then do the seat's work.

**Placement: end of the Monday session.** This gives "Build the model" (§4) a product rather
than only an exposition, uses the overnight gap for design thinking, and — the useful part —
**enforces the commitment gate by the calendar rather than by an honor system.** Materials
unseal in Wednesday's studio. Monday then earns its name twice over: the generative model of the
phenomenon, and the design of the computation.

**The commitment device is `git commit`** — free, timestamped, already in the toolchain.

#### The phase-1 artifact is the model card

§5's four slots — the story, what is unknown, how we pin it down, how it lies to you — *are* a
design document for a probabilistic method. So **one artifact serves both the
computational-thinking instrument and the probabilistic frame**, and no student faces a blank
page: it is four prompts, not an empty file. (Design-from-nothing is where students with the
least background freeze; the card is the scaffold that prevents it.)

By Week 13 each student holds twelve committed model cards plus twelve divergence analyses.

#### Grading: commitment, not correctness

- **Phase 1 is credit for having committed before the gate.** Not graded on quality.
- **Divergence analysis is graded in depth on 3–4 labs**, spot-checked otherwise.

Twelve graded design documents per student will not survive contact with the semester. More
importantly, **a heavily-graded phase 1 stops being safe to be wrong in** — and being safe to be
wrong is exactly the property that makes it usable by students with the least background. State
explicitly on every assignment: *a phase-1 design that misses something the materials caught is
a good outcome.*

**Countermeasure against ritual decay:** if phase 1 is not graded, it risks becoming a box-tick.
Use the **Friday share-out** to give it social stakes instead of grading stakes — "three groups
thought the objective was X, the materials assumed Y; who is right?" This reuses a session that
already exists (§4) and costs nothing extra.

#### Progression: from one hole to many

The seats are training wheels. The intended arc:

| Term position | Phase 2 shape |
|---|---|
| **Early** | One hole, clearly marked, seat named and scaffolded |
| **Middle** | One hole, less scaffolding; seat named |
| **Late** | **Multi-hole studio** — stars on two or three boxes, possibly instructor-directed per group, because students now understand how spec, tests, and code constrain each other |

Late-term multi-hole studios are what the old "Designer as capstone" was reaching for, and they
are a better on-ramp to the synthesis project (design + spec + tests + implementation, every
decision justified) than a single seat would have been. The strip (§8.2) communicates the whole
progression without announcing a new structure.

#### The AI level now varies *within* a lab

Phase 1 is precisely the thinking an agent would happily do for the student. Recommended:

| | AIAS level | Rationale |
|---|:--:|---|
| **Phase 1** | **2 — AI Planning** | Brainstorming allowed; the student develops the ideas. (Level 1 is the stricter alternative — see [fork 4](#9-deferred-forks).) |
| **Phase 2** | **4 — Full AI** | Unchanged: direct the agent, verify it, own the result. |

Mixed levels within a single lab is new for the course and must be stated explicitly on every
assignment. It is also arguably the cleanest one-line statement of the course's ethos: **think
first, unaided; then use the agent freely.**

#### Authoring cost: problem statements that do not leak the spec

This is the real price of the change, and it now applies to **all twelve labs** rather than to a
handful of Designer prompts.

**A problem statement that quietly contains its own decomposition makes phase 1 theater.** The
statement must be a genuine domain question, not a task description:

| ✅ Genuine question | ❌ Leaks the design |
|---|---|
| "Which of these reads are rRNA, and how confident can you be?" | "Implement a k-mer Naive Bayes classifier for rRNA reads." |
| "Do these cells fall into distinct types, and how would you know?" | "Cluster the cells with k-means and pick *k*." |

The existing biological anchors in `docs/schedule.md` are most of the way there; they need
rewriting as *questions* rather than *tasks*. This joins the existing author rule in
[`assignment-framework-authoring.md`](assignment-framework-authoring.md) that every exercise be
hand-verifiable from domain knowledge — both constraints must hold at once, and phase-1 prompts
will be the fussiest part of lab authoring.

#### What happened to the old Type D critique content

Type D ("all three given, critique everything") yielded a summary table rather than a distinct
skill and overlapped heavily with Verifier and Reverse engineer. It is distributed rather than
preserved:

| Old Type D component | New home |
|---|---|
| Correctness beyond what the tests cover | Already the Verifier and Reverse-engineer seats |
| Efficiency (reasoning from reading, not benchmarking) | The standing **compute depth branch** prompt (§7) |
| Composability / fit into a larger pipeline | The compute depth branch, and phase-2 divergence analysis where it bears on objectives |

#### Sequencing consequence for the schedule

`docs/schedule.md` currently assigns types A–D per week, including Type D at weeks 7, 8, 10, and
11 (week 8 is the midterm/consolidation week). With no fourth seat, that column is rewritten as:
**seat per week for the early and middle term, multi-hole studio for the late term** — and the
design phase is not a column at all, because it is every week.

### 8.5 Fix 3 — One bundle, always the same files

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

### 8.6 Fix 4 — Cap the requirement count per lab

The Verifier seat (Type B) currently asks for four distinct kinds of test: hand-calculated
example, synthetic, property-based, and documented expected failure. **Property-based testing
is genuinely advanced** — for a student with little programming background that is a cliff, and
it is exactly the population the framework is supposed to protect.

Recommended: **hand-calculated example tests are the required core** (they are the irreplaceable
part — the component an agent cannot produce without the student already understanding the
problem). Synthetic, property-based, and documented-failure tests become **two-of-three
required, with all three as the compute depth branch.** Same ceiling for strong students, a
reachable floor for everyone.

### 8.7 Withdrawn: the fifth exercise type

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
3. **Fifth exercise type, or a modifier?** *Partially resolved in §8.7:* story ↔ code moves to
   the check-in quizzes rather than becoming either. Revisit only if check-ins prove too small
   to carry it.
4. **AIAS level for the design phase — 2 or 1?** Level 2 (AI Planning: brainstorming allowed,
   the student develops the ideas) is the recommended leaning; Level 1 (No AI) is defensible on
   the grounds that phase 1 is exactly the reasoning an agent would substitute for. Note the
   enforcement asymmetry: Level 1 is not observable here the way it is in a proctored check-in,
   so Level 2 may be the more honest label for the same intent. Phase 2 stays Level 4 either
   way. (§8.4)

**Open dependency, not a fork:** the computational-thinking instrument's **step names** must be
confirmed so the phase-1 template uses that vocabulary rather than a parallel set invented here
(§8.4).

## 10. Pending propagation to student-facing pages

None of the following has been changed yet; recorded so it is not lost.

| What | Where | Note |
|---|---|---|
| **Contact format** is stated as 2 × 75-min lectures + 1 × 1–2 hr lab | `README.md`, `docs/course-design.md`, `docs/schedule.md`, `docs/syllabus.md` | Now **3 × 105-min MWF sessions**; needs updating everywhere it appears |
| **Build / code / break** weekly rhythm | `docs/schedule.md`, `docs/course-design.md` | Replaces the lecture/lab table framing |
| **Seats + the four-box strip** replace letter names | `docs/assignment-framework.md`, `_labs/`, `docs/schedule.md` | Three seats; letters stay as author shorthand in `internal/` |
| **Universal design phase** opens every lab, committed at the end of Monday before materials unseal | `docs/assignment-framework.md`, `docs/course-design.md`, `_labs/lab-overview.md`, `internal/templates/assignment-template.md` | Per §8.4. Biggest structural change; also needs the per-phase AIAS levels stated on every assignment |
| **Biological anchors rewritten as questions, not tasks** | `docs/schedule.md`, `internal/assignment-framework-authoring.md` | Per §8.4 — a leaky problem statement makes phase 1 theater. Interacts with [issue #1](https://github.com/bu-bioinfo/bf550/issues/1) |
| **Late-term multi-hole studios** replace the Type D column | `docs/schedule.md`, `docs/assignment-framework.md` | Per §8.4 progression table |
| **One-bundle file layout** | `docs/assignment-framework.md`, [issue #5](https://github.com/bu-bioinfo/bf550/issues/5) | Also resolves the per-type-bundle gap |
| **Depth branches** | `docs/assignment-framework.md`, `_labs/lab-overview.md` | Plus the "must be useful to others" author rule in `assignment-framework-authoring.md` |
| **Notation decoder** page | new page under `docs/` or `_guides/` | Grows through the term |
| **story → code → notation** rule | `internal/` author guidance | Week 3 lecture currently violates it |
| **Verifier test requirements** relaxed to 2-of-3 + core | `docs/assignment-framework.md` | Per §8.6 |
| **Check-in quizzes** alternate code-reading and story/formula-reading | `docs/assessment-and-ai-policy.md`, `internal/templates/checkin-quiz-template.md` | Per §8.7 |
| **Type D / Reviewer removed** — critique content redistributed | `docs/assignment-framework.md` | Per §8.4; superseded by the universal design phase |
