# Lab Structure in a Computational-Thinking Framework (INTERNAL)

> **Internal working document — not published to the course site** (`internal/` is excluded in
> `_config.yml`). This is the operational companion to
> [`ml-pedagogy-design.md`](ml-pedagogy-design.md): that doc records *why* the labs are shaped
> this way; this one records *how a lab is actually built and run*, and — deliberately — **what
> we have not decided yet.**
>
> **Status: thinking-so-far, not a specification.** The step vocabulary is blocked pending a lab
> consult (§2). Most of §11 is genuinely open. Do not author labs against this document yet.

---

## 1. Where this fits

| Doc | Question it answers |
|---|---|
| [`course-design-rationale.md`](course-design-rationale.md) | Why the course makes the code-literacy bet at all |
| [`ml-pedagogy-design.md`](ml-pedagogy-design.md) | Why the ML content is framed probabilistically, and how it lands across three MWF sessions |
| [`assignment-framework-authoring.md`](assignment-framework-authoring.md) | Existing rules for writing exercises (biological grounding, per-seat sequencing) |
| **this doc** | How an individual lab is structured, staged, and authored under the computational-thinking arc |
| [`examples/`](examples/) | Three playable draft labs — [Week 1](examples/week-01-lab.md) (first lab, Implementer), [Week 4](examples/week-04-lab.md) (early, Verifier), [Week 10](examples/week-10-lab.md) (later, Reverse engineer) — written in the order a student meets them |

The decisions inherited from `ml-pedagogy-design.md` §8 and treated as settled here: **a
universal design phase opens every lab**, there are **three seats** (Implementer, Verifier,
Reverse engineer), the strip communicates which artifact is the student's, and **one deliverable
bundle** is used all term.

## 2. The arc, and the vocabulary problem

The computational-thinking instrument being deployed in other courses in the program runs
roughly:

1. Start from a problem statement
2. Break it into solvable components
3. Define the components as **computable questions**
4. Select appropriate methods for answering those questions
5. Implement

> **BLOCKED — step names.** BF550 should use *the instrument's* names for these steps, not a
> parallel set invented here; cross-course transfer is most of the value and it evaporates if the
> same five moves have two vocabularies. Pending a lab consult. **Everything below uses
> placeholder labels (S1–S5) and will need a find-and-replace pass once the names are
> confirmed.** Tracked in [`open-decisions.md`](open-decisions.md).

A second question rides along with the naming one: **does BF550 use all five steps, or a
subset?** Step 5 (implement) is only the student's work in the Implementer seat, and steps 1–4
are the design phase. It may be cleaner to say BF550's design phase *is* S1–S4 and the seats
distribute S5 and its verification — but that mapping should be checked against how the
instrument actually presents itself.

## 3. Anatomy of a lab

Every lab is two phases separated by a commitment gate, spread across the week:

| When | Phase | What happens |
|---|---|---|
| **Mon, last ~25–30 min** | **Phase 1 — design** | Problem statement only. Students work S1–S4 and **commit** before leaving. |
| *between sessions* | **gate** | Materials unseal Wednesday. The calendar is the enforcement mechanism. |
| **Wed, full studio** | **Phase 2a — divergence** | Compare committed design against the materials. |
| **Wed, remainder** | **Phase 2b — seat work** | Do the seat's job on the starred artifact. |
| **Fri** | **share-out** | Divergences surfaced across groups; depth-branch reports. |

The strip in the lab header shows the state:

```
Phase 1     DESIGN      SPEC      TESTS      CODE
           ★ YOURS    ▨ sealed  ▨ sealed   ▨ sealed

Phase 2     DESIGN      SPEC      TESTS      CODE
          (committed)   given     given    ★ YOURS
```

## 4. Phase 1 — what students actually produce

The artifact is the **model card** (`ml-pedagogy-design.md` §5), which doubles as the design
document because its four slots *are* a design for a probabilistic method:

| Slot | As a design question |
|---|---|
| **The story** | What process produced this data? What am I actually modeling? |
| **What's unknown** | Which quantities do I need to estimate? *(≈ S2/S3 — the computable questions)* |
| **How we pin them down** | What method answers each question, and why that one? *(≈ S4)* |
| **How it lies to you** | What would make this answer wrong? What would I check? |

This is deliberately *not* a blank page. Design-from-nothing is where students with the least
background freeze, and four prompts is the difference between a hard task and an impossible one.

**Committed via `git commit`** — free, timestamped, already in the toolchain.

**Not graded on quality.** Credit is for having committed before the gate. See §7.

## 5. Phase 2a — the divergence analysis

This is the pedagogical engine, and the part that most needs a rubric we do not yet have (§11).
The prompts:

- Where do the materials' implicit objectives differ from the ones you committed to?
- Which of your worries did they handle? Which did they miss?
- Which did they handle that you never considered?
- **Where do you think your design was better, and why?**

That last prompt is not a courtesy. It has to be live, or the exercise teaches students that the
provided materials are the answer key — which is the opposite of what the sealed phase is for.
See the deliberate-imperfection question in §11.

## 6. Phase 2b — the seats

Unchanged from `ml-pedagogy-design.md` §8.3; summarized here so this doc stands alone.

| Seat | Student's artifact | Framing |
|---|---|---|
| **Implementer** | CODE | "You have the spec and the tests. Make it work — and explain every line." |
| **Verifier** | TESTS | "It claims to work. Prove it, with numbers you worked out yourself." |
| **Reverse engineer** | SPEC | "Here is code nobody documented. What is it *supposed* to do, and what did they forget to pin down?" |

## 7. Deliverable bundle and grading

One file layout, every lab, all term (`ml-pedagogy-design.md` §8.5):

| File | Contents | Phase |
|---|---|---|
| `design.md` | The model card / phase-1 design | 1 — **committed before the gate** |
| `spec.md`, `test_*.py`, `impl.py` | The four artifacts; given or authored per seat | 2 |
| `notes.md` | Divergence analysis, then the seat's reflective product (annotation / gap analysis), then a `## Depth` section | 2 |
| `log.md` | Process record — failures and what they taught you | 2 |

Grading posture:

- **Phase 1:** credit for timely commitment. Explicitly *safe to be wrong* — a design that
  misses something the materials caught is a good outcome, and this must be said on the
  assignment, not just believed by the instructor.
- **Divergence analysis:** graded in depth on **3–4 labs**, spot-checked otherwise. Twelve
  deeply-graded design documents per student will not survive the semester.
- **Friday share-out** supplies social stakes so the ungraded weeks do not decay into box-ticking.

AI levels differ by phase — **phase 1 at AIAS 2, phase 2 at AIAS 4** (deferred fork; see
`ml-pedagogy-design.md` §9 fork 4). Whatever we land on must be printed on every assignment,
since mixed levels within one lab is new for the course.

## 8. Progression across the term

| Term position | Phase 2 | Phase 1 |
|---|---|---|
| **Early** | One hole, seat named, heavily scaffolded | Pairs; template heavily prompted |
| **Middle** | One hole, less scaffolding | Individual; template as-is |
| **Late** | **Multi-hole studio** — stars on two or three boxes, possibly instructor-directed per group | Individual; students expected to decompose with less prompting |

The late-term multi-hole studio is the point of the whole structure: students who understand how
spec, tests, and code constrain each other can be handed a realistic mess and told to fix
whatever needs fixing. It is also the direct rehearsal for the synthesis project.

## 9. Authoring rules

Additions to the existing rules in
[`assignment-framework-authoring.md`](assignment-framework-authoring.md):

**Rule 1 — the problem statement must be a question, not a task.** A statement containing its own
decomposition makes phase 1 theater.

| ✅ Genuine question | ❌ Leaks the design |
|---|---|
| "Which of these reads are rRNA, and how confident can you be?" | "Implement a k-mer Naive Bayes classifier for rRNA reads." |
| "Do these cells fall into distinct types, and how would you know?" | "Cluster the cells with k-means and pick *k*." |
| "Which genes best separate responders from non-responders?" | "Rank features by random-forest importance." |

**Rule 2 — the existing hand-verifiability rule still holds.** Every exercise must use a problem
whose correct answer is checkable from domain knowledge without running code. Rules 1 and 2 must
hold *simultaneously*, which is what makes phase-1 prompts the fussiest part of lab authoring.

**Rule 3 — the materials must be worth diverging from: plant productive uncertainty.** If the
provided spec/tests/code are flawless and obvious, the divergence analysis has nothing to bite on.

*Productive uncertainty* is the working term (preferred over "deliberate imperfection," which is
narrower). It covers three distinct kinds of thing, and a good week has some of each:

| Kind | Example (Week 4) |
|---|---|
| **A defensible-but-arguable choice** — not wrong, but a student could reasonably prefer otherwise | Composition-based classification rather than alignment |
| **An unexamined assumption the problem statement quietly contradicts** | Class priors from balanced reference sets, when the library is 70–90% rRNA |
| **A real defect that does not announce itself** | Reads containing `N` raise `KeyError`; overlapping k-mers treated as independent |
| **An absence — something the spec fails to say**, which the student's own agent then decides silently | Week 1: the spec is silent on lowercase, on `N`, and on trailing bases; the agent-written code handles all three anyway |

The **absence** variety is only available when the student authors the code (Implementer seat), and
it may be the strongest form of the technique: the undocumented decision is one the student
produced themselves, so there is no one else to blame and nothing to take on faith. See
[Week 1 §8](examples/week-01-lab.md#8-instructor-notes-not-for-students).

**Author checklist per lab:** at least one item most students should find, at least one that
rewards the depth branches, and **at least one that a strong phase-1 design would have caught** —
that last one is what keeps "where was your design better?" from being a rhetorical question.

Worked instances: [Week 1 §8](examples/week-01-lab.md#8-instructor-notes-not-for-students) (three
absences), [Week 4 §7](examples/week-04-lab.md#7-instructor-notes-not-for-students) (four planted
items) and [Week 10 §7](examples/week-10-lab.md#7-instructor-notes-not-for-students) (seven).

**Author rule 3a — record reachability, not just the defect.** Whether a planted item is *findable*
depends on the fixture, not only on the code. Week 10's empty-cluster defect is unreachable on
generic continuous data and needs duplicate or all-zero rows in the input; that was only discovered
by running it. **Every planted item needs a verified note on how it surfaces**, or the lab ships
with defects nobody can find and instructor hints that fire every time.

**Open:** how much to plant, and whether to tell students it happens (§11 Q10).

**Rule 4 — state the seat and both AI levels in the header**, alongside the strip.

## 10. A worked sketch (Week 4 — rRNA classification)

Included to test whether the structure survives contact with a real week. **Illustrative only.**

**Problem statement given Monday:** *"You have a few thousand short reads from a metatranscriptome
and a reference set of known rRNA and non-rRNA sequences. Which reads are rRNA? How confident can
you be about any individual call?"*

**A plausible phase-1 design:** the story is that each class emits sequence with characteristic
k-mer composition; the unknowns are per-class k-mer probabilities and class priors; we pin them
down by counting in the reference set; it lies to you when a k-mer never appears in training
(zero kills the product), when reads are short, and when the metatranscriptome's class balance
differs from the reference's.

**Materials revealed Wednesday:** spec + tests + code for a k-mer Naive Bayes classifier with
Laplace smoothing, seat = Verifier (student writes tests).

**Divergences we would expect to surface Friday:**

- Most students will not have anticipated the zero-frequency problem before seeing smoothing —
  *this is the good case*, and it is worth naming out loud that the materials taught them
  something their design missed.
- Some will have proposed alignment instead of composition. Worth taking seriously rather than
  correcting: it is a defensible answer to the question as posed, and the reason we chose
  composition (speed, no reference bias at read level) is real content.
- Almost nobody will have specified what "how confident" means. That gap is the on-ramp to
  Week 5's calibration material, and it is better discovered as a hole in their own design than
  presented as a topic.

That third point is the strongest argument for this structure: **the gap in the student's design
becomes the motivation for next week's content.**

## 11. Open questions

Grouped by what blocks what. None of these are decided.

### Blocking — needed before any lab can be authored

1. **Step names and step count** (§2). Blocked on lab consult. Also: does BF550 use all five
   steps or explicitly claim only S1–S4 as the design phase?
2. **How far down should decomposition go?** *Deferred to the team discussion of the
   computational-thinking framework* — this should be settled once, for all courses using the
   instrument, rather than invented here. A 25–30 minute Monday tail cannot sustain decomposition
   to function-level interfaces, so some stopping rule is needed; "down to the point where each
   component is a question you could look up a method for" is a candidate to bring to that
   discussion, not a decision. The example labs sidestep the question with explicit sub-prompts
   under S3, which works but does not scale to twelve weeks of authoring.

### Resolved since first draft

3. ~~**Method selection is degenerate early.**~~ **Resolved.** In the early weeks, "select an
   appropriate method" is a choice from a toolbox holding one item. The step is therefore framed
   as **"what properties would the right method need?"** — answerable with an empty toolbox, and it
   matures into genuine selection as the menu fills. See the framing in
   [Week 4 S3](examples/week-04-lab.md#s3--what-properties-would-the-right-method-need) versus
   [Week 10 S3](examples/week-10-lab.md#s3--what-properties-would-the-right-method-need), where
   students are told to actually choose and justify. Still contingent on Q1: if the instrument
   words this step differently, match its wording while keeping the two-stage progression.

### Structural

4. **Individual or paired phase 1?** Pairs mitigate the freeze problem but dilute individual
   accountability and muddy the commit record. A third option: **design individually, reconcile
   in pairs, then commit** — which adds a cheap peer divergence analysis before the materials
   are even seen. Attractive, untested.
5. **What exactly unseals, and all at once?** A staged reveal (spec → tests → code) would sharpen
   the divergence analysis but adds mechanism and class-management overhead.
6. **How is the gate actually implemented?** Candidates: instructor releases a `phase2/`
   directory Wednesday; materials live on a separate branch or tag; simple in-class distribution.
   The simplest option that works is probably instructor release with no cryptography — the
   calendar and the commit timestamp do the real work. Students who work ahead are a tolerable
   loss.
7. **Does the design phase run all 13 weeks?** *Partly answered by drafting
   [Week 1](examples/week-01-lab.md):* yes, it runs from Week 1 — but **the artifact is not the
   model card that early.** GC content is a *computation*, not a model: there is nothing to
   estimate, so the "what's unknown" slot is near-empty. Week 1 uses the bare S1–S4 worksheet and
   turns the empty slot into the lesson (count versus estimate), which sets up Weeks 3–4. The model
   card proper likely starts Week 3 or 4, so **"twelve model cards" is really nine or ten** — worth
   correcting wherever that figure appears. Week 13 (presentations) remains open.
8. **Is Monday's tail enough time?** 25–30 minutes for S1–S4 plus a commit may be optimistic in
   the early weeks when the template itself is unfamiliar.

### Assessment

9. **We need a divergence-analysis rubric.** Candidate dimensions: did you identify *real*
   differences (not cosmetic ones); did you diagnose *why* they differ; did you judge which is
   better *with justification*; did you honestly name what the materials caught that you missed.
   The last one is the hardest to grade and the most important to reward.
10. **Productive uncertainty — how much, and do we tell them?** *Decided in principle:* yes, plant
    it — see Rule 3 in §9 for the taxonomy and the per-lab author checklist. **Still open:** how
    much per lab, and whether to disclose that it happens. Disclosure invites flaw-hunting and
    could turn each lab into a scavenger hunt; non-disclosure risks students treating the materials
    as authoritative, which is the exact deference the sealed phase exists to break. Middle option
    worth considering: disclose the **policy** once at the start of term and never per-lab.
    *Drafting [Week 1](examples/week-01-lab.md) effectively picks that option* — its §0 tells
    students plainly that the materials sometimes contain arguable choices and sometimes plain
    mistakes, and that arguing with them earns marks. If we want a different disclosure policy,
    Week 1 §0 is the place to change it.

    **A third kind of planted item surfaced while drafting Week 1: an *absence*.** When the seat is
    Implementer there is no code to plant a defect in, so the uncertainty lives in what the *spec
    fails to say* — and the student's own agent-generated code then silently decides it. This is
    arguably the strongest version of the technique, because the student produced the flaw
    themselves. Add it to the Rule 3 taxonomy in §9.
11. **Is computational thinking assessed anywhere unaided?** Check-ins and the midterm currently
    cover code reading and (proposed) story ↔ code. A CT-flavored check-in — "here is a problem;
    give me three computable questions and the method you would use for each" — would be the only
    No-AI window onto design skill. Worth considering; costs check-in space.
12. **How does the synthesis project inherit this?** The project asks for design + spec + tests +
    implementation with every decision justified. It should presumably *be* a full uncapped run of
    the same arc, but the relationship should be stated explicitly rather than left implied.

### Load

13. **Cumulative weekly load.** Model card + divergence analysis + seat work + depth branch,
    every week. Each piece is small; the sum has not been estimated against the 4-credit
    expectation. Needs a dry run before the term.
14. **Does phase 1 get shorter as students get better, or does it decay?** If later cards are
    thinner because students are more fluent, good. If they are thinner because the exercise has
    become ritual, bad. We have no way to tell those apart yet.
