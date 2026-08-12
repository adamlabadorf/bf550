# Future Enhancement: Depth Branches (INTERNAL — DEFERRED)

> **Status: deferred, not rejected.** Depth branches were designed for BF550's first offering and
> **removed before launch** to reduce the number of moving parts in an already-novel course
> architecture. This document preserves the complete design so it can be reintroduced in a later
> semester without re-derivation. Tracked as a GitHub enhancement issue.
>
> Everything below is written in the present tense as a design, not as a plan for year one.

---

## 1. The problem depth branches solve

BF550's founding constraint is a wide range of incoming background — mathematical and
computational — and the requirement to be **challenging across that whole range without anyone
feeling left behind.**

The usual instrument, optional harder problems, fails in a specific way: it quietly brands a
second tier, and it mostly rewards students who were already comfortable. Anyone not doing the
"bonus" work knows exactly where they stand on the single ladder.

Depth branches replace the ladder with **lateral directions**: every extension is a different
*kind* of deeper, not a different *amount*.

## 2. The design

### The three branches

Fixed all term — one stable menu, never a new structure to learn:

| Branch | Standing prompt |
|---|---|
| **Math** | Derive why the estimator for this method is what it is. |
| **Compute** | Make it robust, fast, or scalable — log-space to avoid underflow, vectorize, profile-by-reading, fit it into a pipeline. |
| **Bio** | Which assumption does real data violate, and what does that cost? Design the check that would reveal it. |

The compute branch is also the standing home for efficiency/composability critique (does the
implementation do unnecessary work; would it survive being run over many samples).

### Why students do not sort by ability

The branches deliberately cut across the incoming-skill axes: CS-strong students tend toward
compute, wet-lab students toward bio, math-strong students toward math — **so there is no single
ladder to be low on.** Each student periodically holds knowledge the others need, which is the
opposite of tiering.

Two hard rules keep this honest:

1. **Every branch must be genuinely useful to the others.** A branch nobody else needs to hear
   about is a bonus problem wearing a costume.
2. Branches are presented as *directions*, never as difficulty levels. "Pick by curiosity, not by
   what sounds impressive."

### Cadence and deliverable

- **Six depth sections per term** (not weekly — weekly was the original design and was cut for
  load), student-chosen weeks, **at least one from each branch.**
- Deliverable: a `## Depth` section in the build week's `notes.md` — roughly half a page plus the
  artifact the work produced (a derivation, a benchmark table, a plot from real data).
- Grading: **pass/revise**, not scored. Cheap for TAs; keeps depth from becoming a place students
  grind for points.

### The share-out: what makes depth lateral rather than siloed

Depth only avoids tiering if the findings are **redistributed**. The Share session includes a
share-out where the week's depth work is presented back to the room, so each direction's findings
become common knowledge.

**Scale correction (verified arithmetic, do not lose this):** at 50–60 students, 6 depth sections
each across ~10 eligible weeks means **~33 depth-writers in any given week** — a whole-room
share-out is infeasible. The working design is **pods**: groups of ~6, each pod hearing 2–3 depth
reports, then one 60-second report-out per pod to the room. More students speak, and the format
survives attendance fluctuation.

### Authoring cost

Three branch prompts per problem is the ceiling, not the requirement:

- **Heavy problems** (~6 of 11; see authoring rule 3b): all three branch prompts.
- **Light problems**: two of three. Students need six sections across ten-plus opportunities, so a
  missing branch on some weeks costs nobody anything.
- Productive-uncertainty planting interacts with depth: the per-problem checklist included **"at
  least one planted item that rewards a depth branch"** (e.g., the k-mer independence violation is
  reachable mainly from the bio branch; log-space underflow from compute).

### Textbook hooks

Chapter frontmatter can carry per-concept `depth_hooks` (a math, compute, and bio angle per major
concept), which serve two purposes: prompts for the branch that week, and the tutor skill's
"escalate laterally" behavior — when a student wants more, the tutor offers the three directions
rather than "a more advanced version." *(The tutor's lateral-escalation principle is retained in
year one even with graded depths removed — it is good tutoring independent of the course
mechanism.)*

## 3. Where depth appeared in the course materials (removal inventory)

Removed for year one from:

| Location | What was there |
|---|---|
| `index.md` | "Going deeper, your way" section; depth in the deliverables paragraph |
| `internal/course-structure.md` | §3 Share-session block 2 ("depth share-out"); §5 "two things to learn" (now one) and the bundle's `## Depth` section; §7 grading row |
| `internal/ml-pedagogy-design.md` | §6 "Depth branches: challenge without tiers" (the full rationale, preserved above) |
| `internal/assignment-framework-authoring.md` | Rule 3 checklist item "rewards a depth branch" |
| `internal/textbook-ai-design.md` | Depth branches in the skill's conventions list; lateral escalation reworded to stand alone |
| `internal/computational-thinking-basis.md` | Systems-thinking coverage note (compute branch was its partial home) |

The archived v1 examples (`archive/examples-v1/`) retain their depth sections untouched — they are
worked examples of branch prompts and their instructor notes, useful when reintroducing.

## 4. What year one loses, and the interim story

Removing depth removes the course's only *named* differentiation mechanism. The honest interim
answer for strong students:

- **The design stage has no ceiling.** "How would it lie to you?" rewards exactly as much
  sophistication as a student brings.
- **The divergence analysis has no ceiling** — "where was your design better than ours?" is a
  standing invitation to out-think the materials.
- **Textbook practice problems** (ungraded, with worked solutions) provide unstructured depth.
- The **compute-flavored critique** (efficiency, composability) survives inside the Reverse
  engineer and Implementer products where relevant.

What is genuinely lost: the *redistribution* — the mechanism by which one student's depth became
the room's knowledge — and the explicit signal to strong students that the course has somewhere
for them to go. Watch for boredom in the strong tail in year one; it is the symptom this design
existed to prevent.

## 5. Reintroduction checklist

When adding depth back (target: second offering):

1. Restore the student-facing section (draft preserved in §6 below) and the bundle's `## Depth`
   slot.
2. Restore §7 grading row (pass/revise) — no weight change needed; depth lives inside the
   problems bucket.
3. Add branch prompts to problem materials (3 for heavy, 2 for light) — check the planted
   uncertainty still includes a depth-rewarding item per problem.
4. Stand up the pod-based share-out in the Share session's block 2 (displacing ~25 min of
   design-clinic time — re-verify the Share-session budget).
5. Decide whether `depth_hooks` enter textbook frontmatter (cheap if done during authoring,
   annoying to retrofit — **consider carrying the hooks in chapter frontmatter from the start
   even in year one**, unrendered).
6. Re-run the load arithmetic: depth was cut from weekly to 6/term for load reasons *before* being
   deferred entirely; do not reintroduce at weekly cadence.

## 6. Preserved student-facing text

As published on the front page before removal:

> ## Going deeper, your way
>
> Six times during the term (your choice of weeks, at least one from each), you'll add a
> **depth section** to your build-week write-up:
>
> - **Math** — derive why the estimator is what it is
> - **Compute** — make it fast, robust, or scalable
> - **Bio** — find the assumption real data violates, and what it costs
>
> These are *different directions*, not different difficulty levels. The Share sessions where
> depth work gets shared exist so that the room ends up knowing what each direction found. Pick
> by curiosity, not by what sounds impressive.

---

## 7. GitHub issue — ready to file

> Issues are disabled on the fork and this session cannot reach `bu-bioinfo/bf550`; file the
> following there (label: `enhancement`), then replace this section with a link to the issue.

**Title:** `Future enhancement: depth branches (lateral math/compute/bio extensions)`

**Body:**

> **Depth branches** were designed for BF550's first offering and deliberately **deferred before
> launch** to reduce moving parts in an already-novel course architecture. Full design, rationale,
> and reintroduction checklist: [`internal/future-depth-branches.md`](https://github.com/bu-bioinfo/bf550/blob/main/internal/future-depth-branches.md).
>
> **What:** optional extensions to a build week's write-up in three fixed, *lateral* directions —
> **Math** (derive why the estimator is what it is), **Compute** (make it robust/fast/scalable),
> **Bio** (find the assumption real data violates, and what it costs). Six per term, at least one
> per branch, pass/revise grading.
>
> **Why they exist:** differentiation across a wide incoming-background range **without tiering** —
> the branches cut across the skill axes, so there is no single ladder to be low on, and the Share
> share-out redistributes each direction's findings.
>
> **What year one loses:** the only *named* differentiation mechanism. **Reintroduction trigger:
> boredom in the strong tail.**
>
> **Reintroduction checklist:**
> - [ ] Restore the student-facing section (§6 of the internal doc) and the `## Depth` slot in `notes.md`
> - [ ] Restore the grading row (pass/revise; no weight change — lives inside the problems bucket)
> - [ ] Branch prompts in problem materials (3 heavy / 2 light) + a depth-rewarding planted item per problem
> - [ ] **Pod-based** share-outs in the Share session's block 2 (~33 depth-writers/cycle at 50–60 students; whole-room is infeasible)
> - [ ] Decide textbook `depth_hooks` frontmatter (consider carrying unrendered hooks from year one)
> - [ ] Do **not** reintroduce at weekly cadence — it was cut to 6/term for load before being deferred
>
> Worked branch-prompt examples with instructor notes: `internal/archive/examples-v1/`.
>
> ---
> _Generated by [Claude Code](https://claude.ai/code)_
