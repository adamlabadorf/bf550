# DRAFT EXAMPLE — Week 4 Lab: Is this read rRNA?

> **Internal draft.** Illustrative example of the lab flow, not final material. Instructor notes
> are at the end under [§7](#7-instructor-notes-not-for-students).

```
Phase 1 (Mon)   DESIGN      SPEC      TESTS      CODE
               ★ YOURS    ▨ sealed  ▨ sealed   ▨ sealed

Phase 2 (Wed)   DESIGN      SPEC      TESTS      CODE
              (committed)   given   ★ YOURS     given
```

**Seat this week: Verifier** — "It claims to work. Prove it, with numbers you worked out yourself."

| | |
|---|---|
| **AI level, phase 1** | **AIAS 2 — AI Planning.** Brainstorm with an agent if you like; the ideas and the writing must be yours. |
| **AI level, phase 2** | **AIAS 4 — Full AI.** Use the agent freely. Your hand-calculated expected values are the graded product, and it cannot supply those. |

### Purpose · Task · Criteria

**Purpose.** Every classifier you meet for the rest of this course reports a number that looks
like confidence. This week you find out what that number is actually made of, by testing one.

**Task.** Monday: design an approach to the problem below and commit it. Wednesday: compare your
design to ours, then write a test suite for the implementation we give you.

**Criteria.** Phase 1 is credit for committing on time — it is *not* graded on quality, and a
design that misses something our materials caught is a good outcome, not a bad one. Phase 2 is
graded on your divergence analysis and on whether your tests have expected values you worked out
by hand.

---

## 1. Monday — the problem

You have **5,000 reads of 75 bp** from a metatranscriptome library: total RNA from a mixed
microbial community, sequenced without a poly-A selection step.

You also have two reference sets, each of about 1,200 full-length sequences:

- `rrna_reference.fasta` — known ribosomal RNA genes
- `mrna_reference.fasta` — known protein-coding transcripts

**Which of your 5,000 reads are rRNA? How confident can you be about any individual call?**

Some context you may or may not need: in an unselected metatranscriptome, rRNA commonly makes up
**70–90%** of reads. Your reference sets are roughly balanced. Reads may contain `N` where the
sequencer was unsure.

## 2. Monday — phase 1 worksheet

**Started in the last 10 minutes of Monday** (we read the problem and sketch S1 together);
**finished on your own and committed before Wednesday.** Work in pairs; both partners commit the
same design to their own repo. Budget 30–40 minutes outside class.

> Placeholder step labels (S1–S4) pending vocabulary alignment with the program's
> computational-thinking instrument.

### S1 · The story — what process produced this data?

Describe, in plain language, how a read comes into existence. What is different about how an
rRNA read is produced versus an mRNA read? You are not describing an algorithm yet; you are
describing the world.

*Optional: write ~10 lines of code that generate a fake read from your story.*

### S2 · What is unknown?

Your story has parts you would have to *learn from the reference sets*. List them. For each, say
what it is a quantity **of** — a probability, a count, a rate, a threshold.

### S3 · What properties would the right method need?

You have not been taught a menu of methods to choose from yet, so do not pick one. Instead:
**what would a method have to be able to do to answer this question?** Consider at least —

- What does it take as input, and what must it output for the *"how confident"* half of the
  question to have an answer at all?
- Does it need the reference sequences at prediction time, or only summaries of them?
- 75 bp is short. What does that cost you?
- What has to happen when a read contains something you never saw in the references?

### S4 · How would it lie to you?

Name at least **three** ways your approach could produce a confident answer that is wrong. For
each, say what you would look at to catch it.

### Commit

```bash
git add design.md
git commit -m "Week 4 phase 1: design before materials"
```

**Wednesday's materials do not unseal until this is committed.** The commit timestamp is the
credit.

---

## 3. Wednesday — what we did

Read `spec.md` and `impl.py` below **before** writing anything.

### `spec.md` (excerpt)

> **`train(sequences_by_class, k=4, alpha=1.0, alphabet="ACGT") -> model`**
>
> Estimate a k-mer language model per class. For each class, count every k-mer occurrence across
> that class's sequences, then convert counts to probabilities with Laplace smoothing:
> `p̂(kmer) = (count + alpha) / (N + alpha * K)`, where `N` is the class's total k-mer count and
> `K = len(alphabet)**k` is the vocabulary size. Class priors are estimated as each class's share
> of the input sequences. Returns log-probabilities throughout.
>
> **`classify_read(read, model) -> (label, score)`**
>
> Score the read under each class as `log prior + sum of log p̂(kmer)` over the read's overlapping
> k-mers. Return the winning class label and `score`, **the margin between the best and
> second-best class log-scores — a measure of how confident the call is.**
>
> *Assumes:* every k-mer in `read` is present in the model vocabulary; `len(read) >= k`.

### `impl.py`

```python
import math
import itertools
from collections import Counter


def kmers(seq, k):
    """Overlapping k-mers, left to right."""
    return [seq[i:i + k] for i in range(len(seq) - k + 1)]


def train(sequences_by_class, k=4, alpha=1.0, alphabet="ACGT"):
    vocab = ["".join(p) for p in itertools.product(alphabet, repeat=k)]
    K = len(vocab)
    total_seqs = sum(len(v) for v in sequences_by_class.values())
    model = {"k": k, "logp": {}, "logprior": {}}
    for cls, seqs in sequences_by_class.items():
        counts = Counter()
        for s in seqs:
            counts.update(kmers(s, k))
        N = sum(counts.values())
        model["logp"][cls] = {
            km: math.log((counts[km] + alpha) / (N + alpha * K)) for km in vocab
        }
        model["logprior"][cls] = math.log(len(seqs) / total_seqs)
    return model


def classify_read(read, model):
    k = model["k"]
    scores = {}
    for cls in model["logprior"]:
        lp = model["logprior"][cls]
        for km in kmers(read, k):
            lp += model["logp"][cls][km]
        scores[cls] = lp
    best = max(scores, key=scores.get)
    runner_up = max(v for c, v in scores.items() if c != best)
    return best, scores[best] - runner_up
```

### Divergence analysis — write this first, in `notes.md`

Before you touch the tests. Roughly a page.

1. **Objectives.** What does our `spec.md` treat as the goal? Where does that differ from what
   you committed Monday?
2. **Your S4 list.** Go through it item by item. Which of your failure modes does this code
   handle? Which does it not? Which did you not think of?
3. **`score`.** Our spec calls it "a measure of how confident the call is." You asked in S3 what
   the output would have to be for *"how confident"* to have an answer. **Does this satisfy
   that?** Argue it either way, but argue it.
4. **Where was your design better?** At least one item. This is a real question — our materials
   are not an answer key, and at least one choice in them is arguable. If you think we got
   something wrong, say so and say why.

### Seat work — Verifier

Write `test_classifier.py`. Required:

- **At least three example-based tests with hand-calculated expected values shown in the
  docstring.** Use a deliberately tiny model so the arithmetic is doable — `alphabet="AC"`,
  `k=1`, `alpha=1.0` gives you `K=2`. Worked starter:

  > `train({"rrna": ["AAAC"], "mrna": ["ACCC"]}, k=1, alpha=1.0, alphabet="AC")`
  >
  > rRNA k-mer counts: A=3, C=1, N=4 → `p̂(A) = (3+1)/(4+2) = 2/3`, `p̂(C) = (1+1)/6 = 1/3`
  > mRNA k-mer counts: A=1, C=3, N=4 → `p̂(A) = 1/3`, `p̂(C) = 2/3`
  > priors: one sequence each → `1/2` and `1/2`
  >
  > So `classify_read("AA", model)` scores rRNA at `log(1/2) + 2·log(2/3)` and mRNA at
  > `log(1/2) + 2·log(1/3)`, giving label `"rrna"` and `score = 2·log 2 ≈ 1.386`.

  Do not reuse that one — build your own, including at least one where the two classes are *not*
  balanced.

- **Two of the following three** (all three if you take the compute depth branch):
  - a **synthetic** test — an input you construct to expose one specific behavior, with your reasoning;
  - a **property-based** test — an invariant that must hold for any valid input;
  - a **documented expected failure** — a test that fails, with an explanation of why the
    limitation is real and whether it should be fixed.

Keep `log.md` as you go: every test that failed, and whether the fault was in the spec, your test,
or the code.

### Depth — pick one, add a `## Depth` section to `notes.md`

- **Math** — Show that with `alpha=0` the per-class estimate is the maximum-likelihood estimate.
  Then explain what `alpha=1` does to it and in what sense the result is no longer an MLE.
- **Compute** — The code sums logs per read, per class, per k-mer. Profile-by-reading: where does
  the time go for 5,000 reads? What would you change, and does anything break if you do? Also do
  all three optional test types above.
- **Bio** — Overlapping k-mers of a 75 bp read are strongly dependent on one another, but the
  code adds their log-probabilities as if they were independent. What does that do to `score`?
  Design a check on real data that would reveal it.

---

## 4. Friday — share-out

Come with your answer to divergence question 4 and one item from your S4 list that the code does
*not* handle.

Whole-group: **what is `score` good for?** We will collect the room's answers and hold onto them
— Week 5 is where they get resolved.

## 5. What you hand in

`design.md` (committed Monday) · `test_classifier.py` · `notes.md` (divergence + Depth) · `log.md`

## 6. What we are looking for

| | |
|---|---|
| **Phase 1** | Committed before the gate. Not graded on quality. |
| **Divergence analysis** | Are the differences you found *real* ones? Do you diagnose *why* they differ, not just that they do? Did you name something we caught that you missed? That last one earns credit — it is not an admission of failure. |
| **Tests** | Hand-calculated values in docstrings, shown as arithmetic. A test whose expected value came from running the code is not accepted. |
| **Log** | Evidence you diagnosed failures rather than nudging until things passed. |

---

## 7. Instructor notes (NOT for students)

### Planted productive uncertainty

Four items, in rough order of how many students should find them:

1. **`score` is a log-odds margin, not a probability, and nothing calibrates it.** The spec's
   phrase "a measure of how confident the call is" is doing a lot of unearned work. *Most* of the
   class should feel the friction here even if they cannot name it — divergence Q3 forces the
   confrontation. **This is the deliberate Week 5 on-ramp.** Do not resolve it Friday; collect
   answers and leave it open.
2. **Priors are estimated from reference-set sizes (≈50/50), which have nothing to do with the
   library's actual rRNA fraction (70–90%).** The Monday statement supplies both facts without
   connecting them. A strong phase-1 design catches this; the code does not. **This is the primary
   "your design was better than ours" hook** and the answer to Q4 we are hoping for.
3. **Reads containing `N` raise `KeyError`.** The Monday statement mentions `N`; the spec quietly
   assumes it away. Findable by reading, and a legitimate documented-expected-failure test.
4. **Overlapping k-mers are treated as independent**, inflating `score` by roughly a factor of
   *k*. Only the bio depth branch is likely to reach this. Feeds Week 7's independence discussion.

Also present and *not* planted — genuine underspecification worth accepting if a student finds
it: `len(read) < k` returns the prior difference silently rather than erroring, despite the spec's
stated assumption.

### Timing

**Monday, last 10 min only:** read the problem aloud ~3, sketch S1 together ~5, questions ~2.
S2–S4 out-of-class (~30–40 min). **S3 is the step that overruns** when students do it alone — the
four sub-prompts exist to stop open-ended flailing, and answering three of four is fine.

**Wednesday (105 min):** just-in-time teach ~15 (smoothing, and why a zero is fatal in a product)
· reveal + read ~10 · divergence ~25 · tests ~40 · wrap ~5. **Depth is out-of-class.**

### Risks

- **Pairs will converge on one partner's design.** Acceptable in Week 4. Individual phase 1 from
  roughly Week 7.
- The hand-calculation starter is worked in full on purpose — Week 4 is too early to withhold the
  pattern. By Week 8 give the fixture without the arithmetic.
- **Do not grade Q4 on whether they found item 2.** Grade on whether the argument is coherent.
  A student who argues a *wrong* item was better, well, has done the exercise.
