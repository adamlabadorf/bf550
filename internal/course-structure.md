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
> | [`archive/`](archive/) | Earlier drafts, retained only for the verified problem statements and planted-defect inventories still to be ported forward (§9) |
>
> **Status:** agreed direction; nothing student-facing has been updated yet (§9).

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
| **Fri** | Break the model | **Design clinic** (25) — supervised work + peer read-through | Generalize (15) → critique clinic (35) → depth share-out (25) → wrap (5) |
| **Sun** | | **design *N* committed** | |

Design *N* is launched Monday, incubates all week with a supervised Friday clinic, and commits
Sunday. Its materials unseal the following Wednesday — a three-day seal with no dependency that
breaks if a student misses a session.

### Session budgets

All three fit 105 minutes:

```
Mon   5 check-in + 75 teach/activity + 10 design launch +  5 wrap  = 95  (10 slack)
Wed  15 unseal+read + 30 divergence + 55 produce      +  5 wrap  = 105
Fri  15 generalize + 35 critique + 25 share-out + 25 design clinic + 5 wrap = 105
```

**No Wednesday teach block is needed** — studio work is on last week's topic, already taught, so the
full session goes to the work. Content delivery lands at **~60 min/week explicit plus ~35 min of
content-by-demonstration** in the critique clinic, with the textbook (§8) carrying first exposure.

## 4. The pipeline calendar

```
Wk  1   design D1                                    ← pipeline fills
Wk  2   design D2   |  implement P1
Wk  3   design D3   |  implement P2
 ...
Wk  8   design D8   |  implement P7      ← midterm week, see below
 ...
Wk 12   design D12  |  implement P11
Wk 13               |  implement P12     ← pipeline drains, project ramps
```

Twelve designs, twelve implementations, one problem per week.

**Week 1 is design-only, and that is what makes setup week work.** There is no P0 to implement, so
**Wednesday's studio in week 1 is free for toolchain setup and course orientation** — git, the repo,
the test runner, the agent, the tutor skill, and a walkthrough of how a week works. No other week
can spare a session for this; the pipeline filling provides one.

> **Sequencing detail that matters:** committing `design.md` requires git, so **git setup must land
> before Sunday of week 1.** Wednesday's setup session is the natural place. If a student is still
> stuck, accept the week-1 design by any means (email, paper) rather than let the toolchain gate the
> first design — it is credit-for-committing, and the point is the habit, not the mechanism.

**Week 13 is implementation-only**, winding down as the synthesis project ramps up.

**Week 8 does not stall the pipeline.** The midterm/consolidation week keeps its design slot, and
its design task is a **cross-cutting method-selection problem**: given a biological question, choose
among everything covered in the first half and justify it. That is the highest-value design task in
the course, it doubles as midterm preparation, and it converts the one calendar disruption into an
asset rather than a hole.

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
| `design.md` | The design / model card | Week *N*, committed Sunday |
| `spec.md`, `test_*.py`, `impl.py` | The four artifacts — given or authored per the strip | Week *N+1* |
| `notes.md` | Divergence analysis, the reflective product for the starred box, then a `## Depth` section | Week *N+1* |
| `log.md` | Process record — failures and what they taught | Week *N+1* |

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

| | |
|---|---|
| **Design (week *N*)** | Credit for committing on time. **Not graded on quality** — and this must be stated on the assignment, because being safe to be wrong is what makes the task usable by students with the least background. |
| **Divergence analysis** | Graded in depth on 3–4 weeks, spot-checked otherwise. Twelve deeply-graded designs will not survive the semester. |
| **The starred artifact** | Per the seat: hand-calculated test values, or a reimplementable spec plus gap analysis, or annotated code plus failure log. |
| **Depth branch** | One section in `notes.md`. Lateral, not tiered. |

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
   ([`computational-thinking-basis.md`](computational-thinking-basis.md) §7)
2. **How Bayesian?** Leaning: McElreath's pedagogy and generative framing, not his inference
   machinery. Grid approximation for genuine-posterior cases; full Bayes as a depth branch.
3. **AIAS level for the design stage** — 2 or 1.
4. **Simulation's scope** — see `ml-pedagogy-design.md`; the leaning is to concentrate it in
   weeks 2–4 and keep it as a Friday diagnostic rather than a weekly ritual.
5. **Topic compression** — merge Clustering I+II; compress t-SNE/UMAP to a demo.
6. **How much productive uncertainty per problem, and whether to disclose the policy.**
7. **Two problems in flight** is the stagger's real cost. Fallback if load proves too high: design
   every *other* week (six instead of twelve), at the price of the clean steady state.

**Pending propagation to student-facing pages** — none of this has been written up for students:

| What | Where |
|---|---|
| Contact format: **3 × 105-min MWF**, not 2 × 75 + lab | `README.md`, `docs/course-design.md`, `docs/schedule.md`, `docs/syllabus.md` |
| The **staggered pipeline** and the lab-trails-lecture-by-one-week rule | `docs/schedule.md`, `docs/course-design.md` |
| The **strip** as the one canonical representation; letters A–D retired | `docs/assignment-framework.md`, `_labs/` |
| The **bundle**, and the design/divergence/depth deliverables | `docs/assignment-framework.md` |
| **Reading carries first exposure** at ~2 hr/week, and students must be told | `docs/syllabus.md`, `docs/course-design.md` |
| Biological anchors rewritten as **questions, not tasks** | `docs/schedule.md`, and [issue #1](https://github.com/bu-bioinfo/bf550/issues/1) |
| Per-stage AI levels | `docs/assessment-and-ai-policy.md` |
| **v2 example labs** — port the verified problem statements and planted-uncertainty inventories from [`archive/examples-v1/`](archive/examples-v1/) into the staggered shape | new `internal/examples/` |
