# ⚠ ARCHIVED — Superseded sections of ml-pedagogy-design.md (INTERNAL)

> Extracted from [`../ml-pedagogy-design.md`](../ml-pedagogy-design.md) during the sweep that
> followed the move to the **staggered design/implement pipeline**. The live doc now holds pedagogy
> only; these sections described the *structure*, which is now
> [`../course-structure.md`](../course-structure.md).
>
> Kept because the reasoning is worth re-reading — particularly the §4.1 content-delivery audit
> (which found the original design had budgeted ~45 min/week of exposition against ~150 in a
> conventional course) and the §8 diagnosis of why four lettered exercise types were hard to follow.
> **The mechanics in both are obsolete.** Live equivalents:
>
> | Superseded here | Now lives in |
> |---|---|
> | §4 weekly format, §4.1 session budgets | `course-structure.md` §3 |
> | §8 exercise-type legibility, the strip, seats, bundle | `course-structure.md` §5 |
> | §8.4 universal design phase (within-week, Monday-committed) | `course-structure.md` §1–§3 — now staggered across two weeks |
> | §9 deferred forks, §10 pending propagation | `course-structure.md` §9 and `open-decisions.md` |

---

## 4. Weekly format: 3 × 105 minutes, MWF

Rather than framing this as "one lecture plus two labs," each session gets a distinct **verb**.
The three verbs are the probabilistic modeling workflow itself — which is why the format and
the pedagogy reinforce each other:

| Day | Session | Shape | What it is |
|---|---|---|---|
| **M** | **Build the model** | **3 × [15 min teach + 15 min activity]** → 10 min launching the lab's design phase | The generative story for this week's method, arrived at by simulating it |
| **W** | **Build the code** | **15 min just-in-time teach** → 85 min studio → 5 min wrap; lab materials unseal here | The week's lab on the biological anchor, agent-assisted |
| **F** | **Break the model** | **15 min generalize** → 40 min critique clinic → 30 min share-out → 20 min consolidation | Where it fails: overfitting, leakage, violated assumptions, uncalibrated output |

### 4.1 Where the content actually gets delivered

**This section exists because the first draft of this document did not budget exposition at all,
and the omission was serious.** As originally written, Monday carried ~30 min of exposition plus
~15 min of notation, Wednesday was pure studio, and Friday was described as "critique clinic +
share-out" with no teaching budgeted. That is **~45 min/week — roughly 10 hours across the term,
against ~150 min/week and 32.5 hours in a conventional 2 × 75 lecture course.** A 70% cut to
content delivery, unrecorded. The example labs made it concrete: the
[Week 1](examples-v1/week-01-lab.md) Wednesday plan sums to **125 minutes against a 105-minute
session**, so the studios were over-subscribed before any teaching was added.

Three corrections, in order of what they buy:

**1. Every session opens with a teach block — including Wednesday and Friday.** MWF supplies three
touchpoints where a 2 × 75 course has two; the first draft used one. Wednesday's block is not new
concepts, it is the just-in-time thing today's lab needs. Friday's names the general phenomenon
behind what students just hit in three different labs.

**Friday's critique clinic is content delivery and was mislabeled as discussion.** Breaking a model
in front of the room is *how* overfitting, leakage, and calibration get taught. That is ~40
min/week of content-by-demonstration that the original budget did not count.

**2. Interleave rather than block.** A 105-minute room holds three 15-minute bursts separated by
activity: 45 min of exposition where 30 was budgeted, better retention, and no passive stretch
over 15 minutes.

**3. Move most of the design phase out of class.** Monday was spending 25–30 min on it — in the
session under the most pressure. Instead **Monday ends with ~10 minutes launching it** (read the
problem, sketch S1, answer questions); students finish and commit before Wednesday. Design
benefits from overnight, it is AIAS 2 so agent brainstorming is allowed, and the 10 in-room minutes
preserve the property that actually mattered: nobody faces a blank page alone. This supersedes the
"committed before leaving" instruction in §8.4.

#### The budget

| | Explicit teaching | Everything else | Content/week |
|---|---|---|---|
| **Mon** | 3 × 15 min | 3 × 15 min activity + 10 min design launch | **45 min** |
| **Wed** | 15 min | 85 min studio + 5 wrap | **15 min** |
| **Fri** | 15 min | 40 critique clinic + 30 share-out + 20 consolidation | **15 min + 40 demonstration** |
| | | | **≈75 explicit, ≈115 with the clinic** |

Against ~150 min/week conventional, the gap narrows from 105 min/week to about 35.

#### What absorbs the remaining gap

**Reading carries first exposure.** This is a flipped-classroom bet and should be taken
deliberately, since its failure mode is students not doing it. **Budget ~2 hr/week: one Rethinking
chapter (~90 min) plus one short worked notebook (~30 min).** Cheapest accountability is a
two-question ungraded entry poll opening Monday, which doubles as live information about where to
spend the 45 minutes. It deliberately does *not* touch the check-in quizzes, whose No-AI
code-reading role is load-bearing for assessment.

> **Correction to the format note below.** Its claim that out-of-class reading stays "genuinely
> modest" described reading's *volume* while silently changing its *role* from reinforcement to
> first contact. The volume claim survives (~2 hr/week is modest for a graduate course); the role
> change is real and needs stating to students explicitly, because a student who treats the
> reading as optional will experience Monday as incomprehensible rather than as review.

**Some content lives in the lab materials.** In [Week 4](examples-v1/week-04-lab.md) students learn
Laplace smoothing by *reading the spec and code*, not from a lecture. That is genuine delivery, and
it is why authoring these labs costs more than preparing slides — the prep shifts rather than
shrinking.

**The 13-week topic list probably does not fit unchanged.** Candidates, cheapest first:

| Cut | Frees | Rationale |
|---|---|---|
| **Merge Clustering I + II** (wks 10–11) | ~1 week | If k-means is taught as the hard-assignment limit of a mixture (§6), it is one idea, not two |
| **Compress t-SNE/UMAP** (wk 9) to a demo | ~30–45 min | Expensive to teach properly, cheap to gesture at honestly |
| Week 13 neural nets | — | Already the light frontiers week; leave it |

**Instructor decision, not a design consequence** — recorded so the schedule does not silently
assume 150 min/week of lecture that no longer exists.

### Why Friday is worth protecting

Friday is the session most at risk of being reclaimed for content, and the one to guard hardest:

- It is where the schedule's *"a recurring theme, not a one-time topic"* commitment gets teeth.
  Every method offers a fresh way to get generalization wrong; a standing session means that
  recurrence does not have to be scheduled topic by topic.
- It carries ~55 min/week of content — a 15-min generalizing teach block plus the critique clinic,
  which teaches by demonstration (§4.1). Reclaiming Friday for "lecture" would not add exposition;
  it would trade a more effective delivery mode for a less effective one.
- It is where **depth branches get shared out** (§7), which is what keeps differentiated depth
  from siloing.

### Format note: this is effectively a studio course

At 315 minutes/week of contact, the bulk of student effort lands *in the room*. Out-of-class
reading should stay genuinely modest — a Rethinking chapter is readable in an evening in a way
a PRML chapter is not. Budget out-of-class time for reading plus finishing the Wednesday lab,
and no more.

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

**Placement: launched in the last ~10 minutes of Monday, finished and committed before Wednesday.**
Monday reads the problem aloud, sketches S1 together, and answers questions; students complete
S2–S4 on their own time. The gate is still **enforced by the calendar rather than an honor
system** — materials unseal in Wednesday's studio — and the overnight gap is where design thinking
actually happens.

> **Revised.** An earlier draft ran the *entire* design phase in the last 25–30 minutes of Monday.
> That spent the scarcest resource in the format on the activity least dependent on being in a
> room together; see §4.1 for the budget that forced the change. The 10 in-room minutes preserve
> the property that mattered — nobody faces a blank page alone — at a third of the cost.

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
[`assignment-framework-authoring.md`](../assignment-framework-authoring.md) that every exercise be
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

Recorded here, deliberately **not decided** (see [`open-decisions.md`](../open-decisions.md)):

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
| **Reading carries first exposure**, ~2 hr/week, and students must be told so | `docs/syllabus.md`, `docs/course-design.md`, `_lectures/week-*.md` | Per §4.1. A student who treats it as optional will find Monday incomprehensible rather than review |
| **Per-session teach blocks** (Mon 3 × 15, Wed 15, Fri 15) | `docs/schedule.md`, `docs/course-design.md` | Per §4.1 — the format is not "1 lecture + 2 labs" |
| **Topic compression** — merge Clustering I+II, compress t-SNE/UMAP | `docs/schedule.md` | Per §4.1. **Instructor decision**, tracked in `open-decisions.md` |
| **story → code → notation** rule | `internal/` author guidance | Week 3 lecture currently violates it |
| **Verifier test requirements** relaxed to 2-of-3 + core | `docs/assignment-framework.md` | Per §8.6 |
| **Check-in quizzes** alternate code-reading and story/formula-reading | `docs/assessment-and-ai-policy.md`, `internal/templates/checkin-quiz-template.md` | Per §8.7 |
| **Type D / Reviewer removed** — critique content redistributed | `docs/assignment-framework.md` | Per §8.4; superseded by the universal design phase |

