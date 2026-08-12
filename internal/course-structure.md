# Course Structure — The Staggered Design/Implement Pipeline (INTERNAL)

> **Internal design document — not published** (`internal/` is excluded in `_config.yml`).
> This is the **canonical description of how BF550 is structured week to week.** Where it conflicts
> with an older internal doc, this one wins.
>
> | Companion | Covers |
> |---|---|
> | [`course-design-rationale.md`](course-design-rationale.md) | Why the course makes the code-literacy bet |
> | [`ml-pedagogy-design.md`](ml-pedagogy-design.md) | The probabilistic frame, notation literacy, depth branches, week-by-week ML reframes |
> | [`textbook-ai-design.md`](textbook-ai-design.md) | The AI-forward textbook and its tutor skill |
> | [`assignment-framework-authoring.md`](assignment-framework-authoring.md) | Rules for writing exercises |
> | [`computational-thinking-basis.md`](computational-thinking-basis.md) | What we mean by computational thinking; the literature grounding for the four design steps |
> | [`textbook-implementation.md`](textbook-implementation.md) | How the textbook gets built: toolchain, chapter anatomy, CI, co-design workflow |
> | [`archive/`](archive/) | Earlier drafts, retained only for the verified problem statements and planted-defect inventories still to be ported forward (§9) |
>
> **Status:** agreed direction. The front page, schedule, and assessment pages are published;
> remaining student-facing propagation is tracked in §9.

---

## 1. The core mechanism, in one paragraph

**Students design a solution to a biological problem one week, and meet our solution to it the
next.** Week *N* they receive a problem, work out how they would approach it, and commit that.
Week *N+1* our materials for that problem unseal, they analyse where their approach and ours
diverge, and they produce whichever piece of the solution we deliberately left out. Two problems
are in flight at any time, one week apart, and every week has the same shape.

That is the whole structure. Everything below is either a consequence of it or a way of presenting
it.

## 2. Why the stagger, rather than one lab per week

Compressing design and implementation into a single week forces three goals into conflict:

| Goal | Within one week | Staggered |
|---|---|---|
| **Design needs real time** | ~15–30 min at the end of a session | A full week, with a supervised clinic |
| **The seal needs to hold** | A commitment gate between Monday and Wednesday, unenforceable when a student simply opens the folder | A **week boundary** — coarse, natural, one materials release per week |
| **The schedule must survive disruption** | Hard cross-day dependency; a lost Monday breaks the week | Sessions are independent; a lost session costs its own content only |

The stagger buys a fourth thing it is not aimed at. **A week of separation makes the divergence
analysis better**: students compare against a design they are no longer attached to, after a further
week of instruction. Same exercise, more honest.

### The one-week lag is a feature

Learning Naive Bayes on Monday and implementing it on Wednesday is a great deal to ask, and it
crowds the studio session. Under the stagger: **taught Monday → designed with it fresh that week →
implemented the following week, after it has settled.** Every studio session applies material that
has had a week to consolidate, and the Friday critique clinic is stronger because students are
breaking a method whose code they wrote two days earlier.

**The schedule must state plainly that the lab topic trails the lecture topic by one week**, or it
will confuse everyone including the instructor.

## 3. The week, in steady state

Every week from 2 through 12 is identical in shape:

| | Session | **Problem *N*** (designing) | **Problem *N−1*** (implementing) |
|---|---|---|---|
| **Mon** | Teach topic *N* | Reading check-in (5) → teaching (75, interleaved) → **launch design *N*** (10) → wrap (5) | — |
| **Wed** | Studio | *incubating* | **Materials unseal** + read (15) → divergence analysis (30) → produce the missing piece (55) → wrap (5) |
| **Fri** | Break the model | *(block 2 includes the design clinic)* | **Block 1** (~50): generalize + critique clinic · **Block 2** (~50): depth share-out + design clinic |
| **Sun** | | **design *N* committed** | |

Design *N* is launched Monday, incubates all week with a supervised Friday clinic, and commits
Sunday. Its materials unseal the following Wednesday — a three-day seal with no dependency that
breaks if a student misses a session.

### Session budgets

All three fit 105 minutes:

```
Mon   5 check-in + 75 teach/activity + 10 design launch +  5 wrap  = 95  (10 slack)
Wed  15 unseal+read + 30 divergence + 55 produce      +  5 wrap  = 105
Fri  50 [generalize + critique clinic] + 50 [share-out + design clinic] + 5 wrap = 105
```

**Friday is two blocks, not four activities.** Each block still functions at reduced
attendance, and the share-out is rotational: the ~6 students who did a depth section that week
present. The **Monday reading check-in is telemetry, not assessment** — a short ungraded form
whose job is telling the instructor where to spend the session; the *graded* code-reading
check-ins are biweekly and separate.

**No Wednesday teach block is needed** — studio work is on last week's topic, already taught, so the
full session goes to the work. Content delivery lands at **~60 min/week explicit plus ~35 min of
content-by-demonstration** in the critique clinic, with the textbook (§8) carrying first exposure.

## 4. The pipeline calendar

The topic order is organized by the course's own D2 question — **what is unknown?** — in three
acts, with the parallel D4 escalation (*how would you know you're right?*) getting harder each
act: a standard error → held-out data → no ground truth at all.

| Wk | Act | Topic | Design (this week) | Build (last week's) |
|---:|:--:|---|---|---|
| 1 | I | Course intro; reading code | P1 GC content | — (Wed = toolchain setup) |
| 2 | I | Estimation & uncertainty | P2 differential expression | P1 |
| 3 | I | Bayes; probabilities from counts | P3 species of origin | P2 |
| 4 | II | Naive Bayes (generative) | P4 rRNA classification | P3 |
| 5 | II | Evaluation, CV, leakage, calibration | P5 evaluate the classifier | P4 |
| 6 | II | Logistic regression (discriminative pivot) | P6 variant pathogenicity | P5 |
| 7 | II | Linear regression & regularization | P7 dose–response | P6 |
| 8 | II | Consolidation + **midterm** | P8 method selection | P7 (**light build**) |
| 9 | III | Trees & forests (the honest outlier) | P9 biomarkers | P8 |
| 10 | III | PCA (t-SNE/UMAP as demo) | P10 matrix structure | P9 |
| 11 | III | Clustering: GMM → k-means, validating *k* | P11 cell types | P10 |
| 12 | III | **Act III exam** (Mon) · frontiers/NN (Fri) | **Synthesis project** | P11 |
| 13 | — | Project studio | — | project |

**Eleven weekly problems; the synthesis project is the twelfth design.** The pipeline drains
*into* the project rather than alongside it — one less problem to author, and the project's
design uses the identical move students have made eleven times.

Sequencing choices that carry weight:

- **Regression sits at week 7, adjacent to logistic regression** — the linear/probabilistic
  family is contiguous, and regularization-as-a-prior closes the week-3 smoothing loop while it
  is fresh.
- **Trees sit at week 9, after the midterm.** The midterm then examines a coherent unit (the
  probabilistic supervised family, estimation → regression) from which trees — the method that
  drops the probability story — was always a category error; and the post-midterm week gets
  fresh, intuitive material exactly when a course otherwise sags. Trees also open Act III
  thematically: the first safety net removed.
- **Clustering is one week** (GMM → k-means as one idea), and **t-SNE/UMAP is a demo** inside
  the PCA week, not a treatment.

### The two exams

Each act closes with a secured, no-AI, code-reading exam. **Midterm, week 8**: Acts I–II.
**Act III exam, Monday of week 12**: weeks 9–11 only — frontiers material is exam-exempt,
which keeps week 12's teaching honest as a light session. **Nothing is examined in finals
period**; after Monday of week 12 the term belongs to the project.

Week 12's shape: Mon = Act III exam (~75 min) + project design launch (~30) · Wed = studio,
P11 build · Fri = frontiers demo + project design clinic. Week 13: all three sessions are
project studio.

**Week 1 is design-only, and that is what makes setup week work.** There is no P0 to implement, so
**Wednesday's studio in week 1 is free for toolchain setup and course orientation** — git, the repo,
the test runner, the agent, the tutor skill, and a walkthrough of how a week works. No other week
can spare a session for this; the pipeline filling provides one.

> **Sequencing detail that matters:** committing `design.md` requires git, so **git setup must land
> before Sunday of week 1.** Wednesday's setup session is the natural place. If a student is still
> stuck, accept the week-1 design by any means (email, paper) rather than let the toolchain gate the
> first design — it is credit-for-committing, and the point is the habit, not the mechanism.

**Week 8 does not stall the pipeline.** The midterm/consolidation week keeps its design slot, and
its design task is a **cross-cutting method-selection problem**: given a biological question, choose
among everything covered in the first half and justify it. It doubles as midterm preparation, and
P7's build that week is deliberately light (linear regression is the most hand-calculable build of
the term).

> **Class size is a planning parameter: 50–60 students** (not student-facing). Consequences:
> Friday share-outs must be rotational (~6 presenters/week works at any size); design clinics
> pair-based; grading is TA-staffed (~20 hr/TA/week, with agentic assistance under
> consideration); and **project presentations in any traditional format do not fit** — see
> `open-decisions.md` for the format question.

## 5. What the student actually has to learn

Two things:

1. **Every problem gets designed one week and built the next.**
2. **You pick a depth branch** — math, compute, or bio.

Everything else is a *view* of the first one. The strip, the seat names, the file bundle, and the
model card are four descriptions of a single fact — *which piece is yours this week* — and must be
taught as one thing. Presenting them as four systems is the main way this structure becomes hard to
follow.

**One canonical representation: the strip.** Everything else derives from it.

```
Week N        DESIGN      SPEC      TESTS      CODE
             ★ YOURS    ▨ sealed  ▨ sealed   ▨ sealed

Week N+1      DESIGN      SPEC      TESTS      CODE
            (committed)   given     given    ★ YOURS
```

- The **file bundle** mirrors the strip, one file per box.
- The **seat name** is a label for the starred box — *Implementer* (code), *Verifier* (tests),
  *Reverse engineer* (spec). Good names, memorable, but **not a rotation students must track.**
  Which piece is withheld varies for authoring reasons; the strip already says which.
- The **model card** is what goes in the DESIGN box. Strictly, the DESIGN box always holds the
  four-slot D1–D4 worksheet (§6); it earns the name *model card* from around week 3, once there is
  something to estimate. Weeks 1–2 are computations rather than models, so the "what's unknown" slot
  comes out near-empty — deliberately, since that emptiness is what sets up the count-versus-estimate
  distinction. See `ml-pedagogy-design.md` §5.

### The bundle

| File | Contents | When |
|---|---|---|
| `design.md` | The design | Week *N*, committed Sunday |
| `spec.md`, `test_*.py`, `impl.py` | The four artifacts — given or authored per the strip | Week *N+1* |
| `notes.md` | Divergence analysis, the reflective product for the starred box, the process record (failures and what they taught), and — six times a term — a `## Depth` section | Week *N+1* |

One design file, the starred artifact, one reflective file. There is no separate log.

**Depth sections are six per term, student-chosen weeks, at least one per branch** — not
weekly. This halves recurring load, keeps the lateral-depth machinery, and makes the Friday
share-out rotational (the week's depth-writers present; everyone presents roughly twice a
term).

**"Model card" is internal vocabulary only.** Students see `design.md` and the four questions;
the term never appears in student-facing material. The end-of-term "stack" survives as
*compile your designs* — the on-ramp to the synthesis project.

## 6. Scaffolding the design task

A week of time does not solve the blank page; it relocates it. Five scaffolds, cheapest first — the
textbook (§8) makes the best one nearly free.

1. **A fully worked design in the textbook every week, for an *analogous* problem** — not the one
   being designed. The highest-value scaffold available: students see what "done" looks like before
   attempting it, which is what most reliably prevents freezing.
2. **Progressive prompt removal.** Weeks 1–3: sub-prompts under every step. Weeks 4–8: step names
   only. Weeks 9+: the problem and the model card. **Publish the removal schedule up front**, so it
   reads as growth rather than as the handouts degrading.
3. **The Friday design clinic with peer read-through.** Pairs swap drafts and ask questions — not
   critique, just *"what would your output actually look like?"* Catches the most common failure
   (answering a different question than the one asked) while the instructor is in the room.
4. **A pre-commit self-check.** Four or five questions: have I said what the output is? what would
   count as wrong? what did I have to decide that the problem did not decide for me?
5. **Anonymized prior-year designs, including weak ones, discussed openly.** Available from year
   two. Nothing normalizes "being wrong in week *N* is fine" faster.

### The design steps

Four steps, the same every week. They are also the four slots of the model card
(`ml-pedagogy-design.md` §4), so exposition and design share one template. Grounding in the
computational-thinking literature, and where we depart from it, is in
[`computational-thinking-basis.md`](computational-thinking-basis.md).

| Step | Prompt | Model-card slot |
|---|---|---|
| **D1 · Frame** | What process produced this data? | The story |
| **D2 · Decompose** | What has to be computed or estimated? | What's unknown |
| **D3 · Select** | *Early:* what would the right method need to do? *Later:* which method, and why that one? | How we pin them down |
| **D4 · Anticipate** | How would it lie to you? | How it fails |

The D3 two-stage framing exists because **method selection is degenerate when the toolbox holds one
item.** "What properties would it need?" is answerable with an empty toolbox and matures into real
selection as the menu fills.

## 7. Grading posture

**Weights: weekly problems 30 · check-ins 10 · midterm 15 · Act III exam 15 · synthesis
project 30 · participation 5.** Two secured exams, one per act boundary; the project stays at
30% so the incentive structure and the course's stated philosophy agree. (Supersedes the
weights in issue #2, which predate the Act III exam.)

| | |
|---|---|
| **Design (week *N*)** | Credit for committing on time. **Not graded on quality** — stated on every assignment, because being safe to be wrong is what makes the task usable by students with the least background. |
| **Divergence analysis** | Graded in depth on the ~6 heavy problems (see authoring doc), rubric-checked otherwise. |
| **The starred artifact** | Per the seat: hand-calculated test values, or a reimplementable spec plus gap analysis, or annotated code plus the account of what the agent decided. |
| **Depth** | Six per term, at least one per branch, in `notes.md`. Lateral, not tiered. |
| **Exams** | Midterm (wk 8, Acts I–II) and Act III exam (wk 12 Mon, wks 9–11), both no-AI code reading, 15% each. |
| **Re-entry rule** | A missed design converts to a *hindsight critique* — different prompt, same credit, no pretense the seal held. One missed week costs one week, never more. Published to students. |

Grading is TA-staffed (~20 hr/week per TA), with agentic grading assistance under
consideration — if adopted, it needs its own policy note before the term.

AI levels differ by stage — **design at AIAS 2, week *N+1* work at AIAS 4** (open: see §9). The
split is the cleanest statement of the course's ethos: *think first, unaided; then use the agent
freely.*

**Friday's share-out supplies social stakes** so the ungraded design weeks do not decay into
box-ticking: three groups thought the objective was X, the materials assumed Y — who is right?

## 8. Reading carries first exposure

The format is flipped, deliberately. Monday's 75 minutes are **activation and elaboration of
material already read**, not first delivery.

- **Budget ~2 hr/week**: one textbook chapter plus one short worked notebook.
- **Accountability is the Monday reading check-in** — deliberately low-stakes; its real job is
  telling the instructor live which part of the reading did not land, so the 75 minutes can be spent
  there.
- **This is what makes the structure robust to disruption.** A student who misses a session recovers
  from the textbook rather than from a classmate's notes. That was the original brittleness concern
  and the textbook is the answer to it.

The textbook is therefore not a supplement — it is load-bearing infrastructure. Its design,
including the tutor-skill layer, is in [`textbook-ai-design.md`](textbook-ai-design.md).

> **The textbook contains no graded assignments, by design.** It holds explanation, worked examples,
> and ungraded **practice problems**; the weekly design problems and lab materials are released
> separately. This separation is what lets the textbook be fully open to a student's AI tutor
> without exposing any graded work — see `textbook-ai-design.md` §1. Keeping it clean is a standing
> authoring constraint, not an incidental fact: **a lab problem that migrates into the textbook
> breaks the tutor's safety property.**

## 9. Open and pending

**Deferred forks** (also in [`open-decisions.md`](open-decisions.md)):

1. **Decomposition stopping rule** — D2 needs a rule students can apply for how far down to go.
   Candidate: *down to the point where each component is a question you could look up a method for.*
   ([`computational-thinking-basis.md`](computational-thinking-basis.md) §8)
2. **How Bayesian?** Leaning: McElreath's pedagogy and generative framing, not his inference
   machinery. Grid approximation for genuine-posterior cases; full Bayes as a depth branch.
3. **How much productive uncertainty per problem**, and per-problem disclosure (policy disclosure
   at term start is settled).
4. **Two problems in flight** is the stagger's real cost. Fallback if load proves too high: design
   every *other* week, at the price of the clean steady state.
5. **Synthesis project format at 50–60 students** — traditional presentations do not fit;
   candidate formats in `open-decisions.md`.

Settled since earlier drafts of this list: design stage is **AIAS 2**; simulation front-loads
weeks 2–4 + Friday diagnostic; clustering is one week and t-SNE/UMAP a demo (both baked into the
§4 calendar).

**Pending propagation to student-facing pages** — none of this has been written up for students:

| What | Where |
|---|---|
| ~~Front page~~ · ~~schedule~~ · ~~assessment policy~~ | `index.md`, `docs/schedule.md`, `docs/assessment-and-ai-policy.md` | **Done** — rhythm, acts calendar, weights, exams, re-entry rule, per-stage AI levels all published |
| Contact format + rhythm on the remaining pages | `README.md`, `docs/course-design.md`, `docs/syllabus.md` | Still say 2 × 75 + lab and "weekly labs" |
| The **strip**; letters A–D retired; the bundle | `docs/assignment-framework.md`, `_labs/` | Full rewrite needed |
| `_lectures/week-*.md` topics | all 13 files | Still ordered by the old sequence |
| **Reading carries first exposure** at ~2 hr/week, stated to students | `docs/syllabus.md`, `docs/course-design.md` | |
| **v2 example problems** — port verified statements + planted-uncertainty inventories from [`archive/examples-v1/`](archive/examples-v1/) into the staggered shape | new `internal/examples/` | |
