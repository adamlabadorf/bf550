# DRAFT EXAMPLE — Week 1 Lab: Where does the GC content change?

> **Internal draft.** Illustrative example of the lab flow at the *start* of term, not final
> material. Instructor notes at the end under [§8](#8-instructor-notes-not-for-students).
>
> Read alongside [`week-04-lab.md`](week-04-lab.md) and [`week-10-lab.md`](week-10-lab.md). Week 1
> is deliberately the odd one out — see [§8](#8-instructor-notes-not-for-students) for what is
> different and why.

```
Phase 1 (Mon)   DESIGN      SPEC      TESTS      CODE
               ★ YOURS    ▨ sealed  ▨ sealed   ▨ sealed

Phase 2 (Wed)   DESIGN      SPEC      TESTS      CODE
              (committed)   given     given   ★ YOURS
```

**Seat this week: Implementer** — "You have the spec and the tests. Make it work — and be able to
explain every line."

| | |
|---|---|
| **AI level, phase 1** | **AIAS 2 — AI Planning.** Brainstorm with an agent if you want; the ideas and the writing are yours. |
| **AI level, phase 2** | **AIAS 4 — Full AI.** Let the agent write the code. You are accountable for explaining it and for the failure log. |

### Purpose · Task · Criteria

**Purpose.** Two things at once. You will do a small, genuinely easy computation on DNA — and
you will find out that "compute the GC content" was never a complete instruction. That discovery
is the thesis of this course, and this week is where it lands.

**Task.** Monday: design an approach to the question below and commit it. Wednesday: compare your
design against the specification we hand you, then get a working implementation — with an agent if
you like — and account for every decision inside it.

**Criteria.** Phase 1 is credit for committing on time; it is **not graded on quality**. Phase 2 is
graded on your annotation, your failure log, and your divergence analysis — not on whether the code
works. (It will work. That is not the hard part, and this course is not about the part that isn't
hard.)

---

## 0. First, how a lab works

Every lab this term has the same shape. You will stop needing this section after about Week 3.

**Monday you design, before you see anything of ours.** You get a biological question and nothing
else — no code, no specification, no tests. You write down how you would approach it and you
**commit that to git.** The commit timestamp is what earns the credit; the quality is not assessed.

**Wednesday our materials unseal, and you compare.** The four boxes in the strip above — design,
specification, tests, code — are the four pieces of any computational solution. Each week you get
some of them and you produce one. The star shows which one is yours this week. That is all the
strip means; there is nothing else to memorize.

**We are not an answer key.** Our materials are written by people, in a hurry, with opinions. Some
weeks they contain a choice you could reasonably disagree with. Some weeks they contain a plain
mistake. **You are expected to argue with them**, and there are marks for doing it well. If you
find yourself assuming our version must be right because we handed it to you, that is the habit
this course exists to break.

**Friday we compare across the room** and you report on one optional "depth" extension you chose.
The depth options are different *kinds* of harder, not different *amounts* — one is mathematical,
one is computational, one is biological. Pick by what you want to get better at, not by what you
think is most advanced. Nobody is expected to pick the same one every week, and no branch is the
"top" one.

**You will use an AI coding agent, and that is fine.** Every assignment tells you what level of AI
use is expected. The work we grade is the part an agent cannot do for you: deciding what the
problem is, deciding what correct means, and being able to say what the code in front of you
actually does.

---

## 1. Monday — the problem

You have a **50 kb stretch of bacterial genome** as a single FASTA record.

Bacterial genomes are not uniform in base composition. Horizontally transferred regions,
prophages, and pathogenicity islands frequently differ in GC content from the host genome around
them — which makes local GC content a cheap first screen for "this piece of DNA may have come from
somewhere else."

**Where along this sequence does the GC content change? How would you present the answer to a
collaborator, and how would you avoid pointing them at something that isn't real?**

Some context you may or may not need: this FASTA came from a public genome browser download.
Sequencing centers use `N` where a base could not be called. Some genome files use lowercase
letters to mark regions flagged as repetitive.

## 2. Monday — phase 1 worksheet

**We start this together in the last 10 minutes of Monday** — we will read the problem, do S1 on the
board for a *different* problem (reverse complement) so you can see the shape, and take questions.
**You finish S2–S4 on your own and commit before Wednesday.** Work in pairs; each partner commits
the same design to their own repo.

This is the only assignment all term with no wrong answers available, so spend the time it deserves
and no more — 30 to 40 minutes is right.

> Placeholder step labels (S1–S4) pending vocabulary alignment with the program's
> computational-thinking instrument.

### S1 · The story — what process produced this data?

How does a stretch of genome come to have a GC content at all, and why would it differ from one
region to the next? You are not describing an algorithm. You are describing what is going on in the
biology that makes this question worth asking.

### S2 · What is unknown?

List the quantities you would have to compute or estimate from the data.

> **This box is going to look strange this week, and that is on purpose.** For most of this course
> the unknowns are things you *estimate* — quantities you can never see directly and can only
> guess at from data, with an error bar. This week, almost everything you need is something you can
> just *count*. Notice how short your list is. Write down which items are counted and which — if
> any — are guessed at.
>
> Keep this page. In Week 4 you will fill in the same box for a problem where nothing can simply
> be counted, and the difference between those two weeks is most of what this course is about.

### S3 · What properties would the right method need?

You have not been taught a menu of methods, so do not pick one by name. Instead: **what would an
approach have to be able to do** to answer the question as asked? At least —

- The question says "where does it change." What does your output have to look like for
  *"where"* to have an answer? A number? A list? A plot? Be concrete.
- You will have to look at some amount of sequence at a time. What decides how much?
- What would make two people, both doing this correctly, get different answers?

### S4 · How would it lie to you?

Name at least **three** ways this could point your collaborator at a region that isn't really
different from its surroundings. For each, say what you would look at to catch it.

### Commit

```bash
git add design.md
git commit -m "Week 1 phase 1: design before materials"
```

**Wednesday's materials do not unseal until this is committed.** If you get stuck on the mechanics
of git, ask — this week the toolchain is part of the lab, not a prerequisite for it.

---

## 3. Wednesday — setup (first 25 minutes)

Before the materials: get your environment working. Clone your lab repo, confirm you can run the
test suite (it will fail — there is no implementation yet, that is correct), and confirm your
coding agent responds. Ask for help early and loudly. **Nobody is behind for needing help with
this**, and everything after this point depends on it.

## 4. Wednesday — what we did

Here is our specification and our test suite. **Read both before writing anything.**

### `spec.md`

> **`sliding_gc(seq, window=100, step=10) -> list[tuple[int, float]]`**
>
> Report the GC fraction of successive windows along `seq`.
>
> - `seq` — a DNA sequence.
> - `window` — number of bases per window.
> - `step` — number of bases to advance between windows.
>
> Returns a list of `(start, gc_fraction)` pairs, where `start` is the 0-indexed position of the
> window's first base and `gc_fraction` is the proportion of bases in that window which are G or C.
> Pairs are returned in increasing order of `start`.
>
> **`gc_content(seq) -> float`**
>
> The proportion of bases in `seq` which are G or C.

### `test_gc.py`

```python
from impl import sliding_gc


def test_all_gc():
    """Every base is G or C, so every window is 1.0."""
    assert sliding_gc("GCGCGCGCGC", window=5, step=5) == [(0, 1.0), (5, 1.0)]


def test_all_at():
    """No base is G or C, so every window is 0.0."""
    assert sliding_gc("ATATATATAT", window=5, step=5) == [(0, 0.0), (5, 0.0)]


def test_split_sequence():
    """First window all G, second all A."""
    assert sliding_gc("GGGGGAAAAA", window=5, step=5) == [(0, 1.0), (5, 0.0)]


def test_overlapping_windows():
    """Sliding one base at a time across the G/A boundary: 5/5, 4/5, 3/5."""
    assert sliding_gc("GGGGGAAAAA", window=5, step=1)[:3] == [(0, 1.0), (1, 0.8), (2, 0.6)]
```

### Divergence analysis — write this first, in `notes.md`

Before you write any code. Half a page is plenty this week.

1. **Objectives.** What does our spec treat as the goal? Monday's question asked where the GC
   content *changes* — does this specification answer that question, or a smaller one?
2. **Your S4 list.** Which of your three failure modes does this specification address? Which does
   it say nothing about?
3. **The three facts from Monday.** The problem statement mentioned that this file came from a
   public browser download, that `N` marks uncalled bases, and that some files mark repeats in
   lowercase. **Find where the specification tells you what to do about each of those.** Write down
   what you find.
4. **Where was your design better?** At least one thing. This is a real question, not a courtesy.

### Seat work — Implementer

Get `impl.py` written so that `test_gc.py` passes. **Use your agent for this** — that is the point
of Level 4. Then do the part that is actually graded:

**a. Annotate it.** Every non-trivial line gets a comment saying what it does. Not what it *is* —
what it *does*, and why it is there. If you cannot explain a line, you are not finished; ask the
agent to explain it, then write the explanation in your own words.

**b. Answer the question this lab is really about.** In `notes.md`, under a heading
`## What my agent decided for me`:

> Your specification did not say what to do with `N`, with lowercase letters, or with the bases at
> the very end of the sequence that don't fill a whole window. **Your code does something about
> all three anyway.** Find out what. For each of the three:
>
> - What does your implementation actually do?
> - Was that a decision you made, or one the agent made silently on your behalf?
> - Is it defensible? What would the alternative be, and who would care about the difference?

Test your own code on `"GGGGgggg"`, on `"GGGNNNNN"`, and on a sequence whose length is not a
multiple of `step`. Report what happens. Some of what you find will be *wrong* — say so.

**c. Keep `log.md`.** Every test that failed on the way, and whether the fault was in the spec,
the test, or the generated code. If nothing ever failed, say that, and say what you think that
means.

### Depth — pick one, add a `## Depth` section to `notes.md`

Small this week. Twenty minutes each, roughly. Pick by curiosity.

- **Math** — A window of 100 bases with 50 G/C gives 0.50. A window of 10 bases with 5 G/C also
  gives 0.50. Are you equally sure about those two numbers? Argue it in words — no formulas needed
  — and say what that implies about choosing `window`.
- **Compute** — The implementation recounts every window from scratch, so a step of 1 recounts 99
  bases it already counted. Describe a way to avoid that. You do not have to implement it. What
  would you have to be careful about?
- **Bio** — Download or take a real bacterial genome region and run your code on it. Do the peaks
  and valleys look like something biological, or like something about your window size? Change
  `window` by 10× in each direction and report what happens to your answer.

---

## 5. Friday — share-out

Bring: what your agent decided about `N` on your behalf, and whether you agree with it.

We will collect the room's answers on the board. **Expect them to disagree with each other**, from
code that all passed the same tests. That is the finding.

Then, briefly: everyone says which depth branch they picked and one sentence about what they found.
You will hear all three. Over the term, try all three.

## 6. What you hand in

`design.md` (committed Monday) · `impl.py` (annotated) · `notes.md` (divergence + agent decisions
+ Depth) · `log.md`

## 7. What we are looking for

| | |
|---|---|
| **Phase 1** | Committed before the gate. Not graded on quality. Genuinely. |
| **Divergence** | Question 3 above all: did you notice that the specification is silent on all three of the facts we gave you Monday? |
| **Annotation** | Can you account for every line? A line you cannot explain is the only real failure available in this lab. |
| **Agent decisions** | The heart of it. Three behaviors, honestly described, with a judgment about each. "I hadn't realized it did that" is a fine and creditable answer. |
| **Log** | Evidence of diagnosis rather than nudging until green. "Nothing failed" is acceptable if you say what that tells you. |

**Not graded:** whether your code is elegant, whether you wrote it yourself, how fast you finished.

---

## 8. Instructor notes (NOT for students)

### What is different about Week 1, and why

| | Weeks 4–10 | **Week 1** |
|---|---|---|
| Where the productive uncertainty lives | In the provided code | **In the provided spec** — the seat is Implementer, so there is no code to plant it in |
| The planted item | A defect or arguable choice to find | **An absence** — three things the spec fails to say |
| Phase-1 demo | None | **Modeled on the board first**, on a different problem |
| S2 (unknowns) | The substance of the week | **Deliberately near-empty**, and that is the lesson |
| Meta-content | None | **§0 introduces the whole machinery**; drop it by Week 3 or 4 |
| Toolchain | Assumed | 25 min of Wednesday is setup |
| Depth branches | 40–60 min | ~20 min, one framed as "no formulas needed" |
| Failure log | Expected to have entries | **May legitimately be empty** — and the reflection on why is the point |

### The planted productive uncertainty — an absence, not a defect

The Monday statement deliberately supplies three facts it never uses: browser-download provenance,
`N` for uncalled bases, lowercase for repeat-masked regions. The spec is then silent on all three,
and the tests use only clean uppercase input at exact multiples of `step`. So:

1. **Lowercase.** `seq.count("G")` misses `g`. A soft-masked repeat region reads as GC ≈ 0 — a
   dramatic, entirely artefactual "compositional shift" of exactly the kind the biological framing
   says to look for. **This is the best item in the lab**; it is domain-real, hand-findable, and
   it makes the artefact look like the signal.
2. **`N` in the denominator.** "Proportion of bases which are G or C" over `len(seq)` counts `N`
   against you; over called bases only, it does not. **Both are defensible** — this is a genuine
   undocumented decision rather than a bug, which is exactly the distinction we want established in
   Week 1.
3. **Trailing bases.** With `window=100, step=10`, a 50,005 bp sequence never reports on its final
   few bases; no window covers them and nothing says so. Silent 3′ data loss.

Whatever the agent emits will pass all four provided tests while deciding all three of these
silently. **That is the designed experience.** The lab is engineered so that success on the visible
criteria coexists with three undocumented decisions — and then asks the student to go find them.

**Verified** against the obvious implementation (`(seq.count("G") + seq.count("C")) / len(seq)`
with `range(0, len(seq) - window + 1, step)`) — all four provided tests pass, and:

| Absence | Input | Result | Should be |
|---|---|---|---|
| Lowercase | `gc_content("GGGGgggg")` | `0.5` | `1.0` |
| Lowercase | `gc_content("gggggggg")` | `0.0` | `1.0` |
| `N` denominator | `gc_content("GGGNNNNN")` | `0.375` | `1.0` over called bases — *or* `0.375`, defensibly |
| Trailing | 50,005 bp, `window=100, step=10` | last window starts at 49,900, covers to 50,000 | final **5 bases** appear in no window, silently |

The lowercase numbers are the ones to put on the board Friday. A fully soft-masked region reporting
GC = 0.0 is the artefact that looks exactly like the signal the biological framing told students to
hunt for.

### Why GC content, and why it must stay this easy

Week 1 has to isolate one variable: the machinery of the course. If the biology or the computation
is also hard, students cannot tell which thing is confusing them. GC content is reasoning every
student can do regardless of background — and the sliding window is the smallest problem that still
has real specification decisions hiding in it.

Resist the urge to make this more interesting. It is supposed to be a problem where students feel
competent and *then* discover that competence was not sufficient.

### On S2 being nearly empty

This is a deliberate setup for Weeks 2–4 and worth protecting. GC content is a **computation**;
Naive Bayes is a **model**. The distinction — quantities you count versus quantities you estimate
with uncertainty — is the spine of the probabilistic frame, and Week 1 is where students get a
concrete "before" to compare against. Say the words *count* and *estimate* out loud Monday and
then leave them alone until Week 3.

**Consequence for the artifact:** the model card does not fit Week 1, since there is nothing to
estimate and no way for the method to be *statistically* wrong. Week 1 uses the S1–S4 worksheet
directly. The model card proper should probably start at Week 3 or 4 — the "twelve model cards"
figure elsewhere in the design docs is closer to nine or ten.

### Timing

**Monday, last 10 min only:** read the problem aloud ~3, board demo of S1 on reverse complement ~5,
questions ~2. S2–S4 and the commit are out-of-class (~30–40 min). Do *not* attempt the full
worksheet in the room — see `ml-pedagogy-design.md` §4.1.

**Wednesday (105 min):** just-in-time teach ~10 · toolchain setup ~20 · read materials ~10 ·
divergence ~15 · implement ~15 · annotate ~15 · agent-decisions ~15 · wrap ~5. **Depth moves
out-of-class this week** — the 20 min it needs does not exist in Week 1.

> **This plan was over budget and had to be cut.** An earlier draft summed to **125 minutes against
> a 105-minute session** (25 setup + 10 read + 15 divergence + 20 implement + 15 annotate + 20
> agent-decisions + 20 depth). Week 1 is the tightest session of the term because toolchain setup
> is real and unskippable. If setup runs long, **cut the implement block** — the agent can produce
> passing code faster than the estimate assumes, and the annotation is what is graded.

Have a second instructor or TA floating for setup; it will overrun for someone.

### Risks

- **The three planted absences are only findable because Monday named them.** If the Monday
  statement is trimmed for time, remove the matching divergence prompt too, or the lab becomes a
  guessing game. These are coupled.
- **"Nothing failed, so I have nothing to log"** will happen and is legitimate. Handle it as
  content, not as a deficiency: an agent that produces passing code on the first try has told you
  nothing about whether the code is right, which is precisely why the annotation and the
  agent-decisions section exist.
- **Some students will already know all of this.** Their version of the lab is the compute depth
  branch plus a genuinely rigorous answer to item 2 (the `N` denominator question has a real
  literature behind it). Do not let them coast on finishing early; the annotation standard is the
  same for everyone.
- **§0 will feel long to strong students.** Acceptable cost in Week 1. It is the only place the
  course explains itself in full, and the students who need it need it badly.
- **Disclosure policy.** §0 tells students outright that our materials sometimes contain mistakes
  and arguable choices. That is the "disclose the policy once, at the start of term" option from the
  open questions — **Week 1's §0 is where that disclosure would live**, and drafting it here commits
  us to that choice unless we revisit it.
