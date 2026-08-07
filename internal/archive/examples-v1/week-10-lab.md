# DRAFT EXAMPLE — Week 10 Lab: Are these cells of different types?

> **Internal draft.** Illustrative example of the lab flow at a *later* term position, not final
> material. Instructor notes at the end under [§7](#7-instructor-notes-not-for-students).
>
> Read alongside [`week-04-lab.md`](week-04-lab.md) — the differences between them are the point.

```
Phase 1 (Mon)   DESIGN      SPEC      TESTS      CODE
               ★ YOURS    ▨ sealed  ▨ sealed   ▨ sealed

Phase 2 (Wed)   DESIGN      SPEC      TESTS      CODE
              (committed) ★ YOURS     given     given
```

**Seat this week: Reverse engineer** — "Here is code nobody documented. What is it *supposed* to
do, and what did they forget to pin down?"

| | |
|---|---|
| **AI level, phase 1** | **AIAS 2 — AI Planning.** |
| **AI level, phase 2** | **AIAS 4 — Full AI.** Your spec and your gap analysis are the graded product. |

### Purpose · Task · Criteria

**Purpose.** Unsupervised methods will hand you an answer no matter what you feed them, and there
is no accuracy number to catch you. This week you work out what a clustering result would have to
do to earn belief.

**Task.** Monday: design an approach and commit it. Wednesday: recover the specification for the
implementation we give you, and find what it leaves unpinned.

**Criteria.** Phase 1: committed on time, not graded on quality. Phase 2: the **gap analysis is
weighted more heavily than the spec** — finding what is underspecified shows more than
transcribing what is there.

---

## 1. Monday — the problem

You have single-cell RNA-seq for **2,000 cells × 500 genes**, as a matrix of UMI counts. Library
sizes vary from about 1,100 to 34,000 UMIs per cell. The tissue is one a collaborator believes
contains "maybe four or five" cell types, but nobody has annotated it.

**Do these cells fall into distinct types? If so, how many, and how would you know you were
right?**

## 2. Monday — phase 1 worksheet

`design.md`, **started in the last 10 minutes of Monday and committed before Wednesday.**
**Individually this week** — no pairing. Budget 30–40 minutes outside class.

### S1 · The story

What process produced this matrix? Your story has to reach from *"a cell is of some type"* to
*"this row of integers."* Be specific about where the integers come from and what makes two cells
of the same type produce different rows.

### S2 · What is unknown?

There are more unknowns here than in a supervised week, and one of them is unusual. List them all,
and mark which are **parameters** you would estimate versus **structural choices** you would have
to make before estimation could begin.

### S3 · What properties would the right method need?

By now you have a real menu — you have seen generative classifiers, discriminative ones, trees,
and dimensionality reduction. So this week, actually choose, and justify it. Address at least:

- Your story in S1 implies a notion of "similar cells." What is it, concretely, and does it
  operate on the counts as given?
- The collaborator says "maybe four or five." Is that an input to your method or an output of it?
  What changes depending on which?
- **How would you know the answer is wrong?** There are no labels. Nothing will error.

### S4 · How would it lie to you?

At least **four** ways, and for each, the check that would catch it. At least one must be a way
the method returns a *clean, plausible, entirely spurious* answer.

### Commit

```bash
git add design.md && git commit -m "Week 10 phase 1: design before materials"
```

---

## 3. Wednesday — what we did

You get `impl.py` and `test_cluster.py`. **There is no spec — you are writing it.**

### `impl.py`

```python
import random


def dist2(a, b):
    return sum((x - y) ** 2 for x, y in zip(a, b))


def kmeans(X, k, n_iter=50):
    centroids = random.sample(X, k)
    for _ in range(n_iter):
        labels = [
            min(range(k), key=lambda c: dist2(x, centroids[c])) for x in X
        ]
        for c in range(k):
            members = [X[i] for i, lab in enumerate(labels) if lab == c]
            centroids[c] = [sum(v) / len(v) for v in zip(*members)]
    return labels, centroids


def within_cluster_ss(X, labels, centroids):
    return sum(dist2(x, centroids[lab]) for x, lab in zip(X, labels))
```

### `test_cluster.py`

```python
import random
from impl import kmeans, within_cluster_ss


def test_two_obvious_blobs():
    """Points at (0,0)-ish and (10,10)-ish must split 3/3."""
    random.seed(0)
    X = [[0, 0], [0, 1], [1, 0], [10, 10], [10, 11], [11, 10]]
    labels, _ = kmeans(X, k=2)
    assert labels[:3] == [labels[0]] * 3
    assert labels[3:] == [labels[3]] * 3


def test_ss_decreases_with_more_clusters():
    random.seed(0)
    X = [[0, 0], [0, 1], [1, 0], [10, 10], [10, 11], [11, 10]]
    _, c2 = kmeans(X, k=2)
    l2, c2 = kmeans(X, k=2)
    l3, c3 = kmeans(X, k=3)
    assert within_cluster_ss(X, l3, c3) <= within_cluster_ss(X, l2, c2)


def test_centroids_have_right_dimension():
    random.seed(0)
    X = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
    _, centroids = kmeans(X, k=2)
    assert all(len(c) == 3 for c in centroids)
```

### Divergence analysis — `notes.md`, before the spec

1. **Objectives.** What question does this code answer? Is it the question you were asked Monday?
   Be precise about the difference — it is larger than it looks.
2. **Your S2 list.** Which unknowns does this code estimate? Which does it require you to have
   already decided? Which does it not address at all?
3. **Your S4 list.** Which of your failure modes would this code exhibit *without raising an
   error*? Note the tests do not catch them either.
4. **Where was your design better?** At least one, argued.

### Seat work — Reverse engineer

Write `spec.md`, precise enough that someone could reimplement `kmeans` and `within_cluster_ss`
without seeing the code. Then, in `notes.md`:

- **Explain every edge case the tests cover, and why it is there.** Include what
  `test_ss_decreases_with_more_clusters` is actually asserting — and whether the property it
  claims is guaranteed, usually true, or neither.
- **Identify at least four behaviors the tests do not cover**, and propose a test for each.
  At least two must be cases where the code produces a wrong or arbitrary answer rather than
  crashing.
- **Note everything ambiguous.** Where does the code make a choice the spec would have to
  legislate, that a reimplementer could reasonably get differently?

### Depth — one, in a `## Depth` section

- **Math** — Show that the assignment step and the update step each never increase
  within-cluster sum of squares, and explain why that means the loop converges but not that it
  finds the best answer. Then state what `n_iter=50` is standing in for.
- **Compute** — Fix the defects you found, without changing the interface. Then: the code is
  O(n·k·d) per iteration with Python-level loops; what does 2,000 × 500 cost, and what is the
  smallest change with the largest effect? (Efficiency and composability critique lives here.)
- **Bio** — The matrix is raw UMI counts with a 30× library-size range, and `dist2` is squared
  Euclidean. Work out what this clusters cells *by*. Propose the preprocessing you would insist on,
  and say which of your S4 failure modes it fixes and which it does not.

### Optional extension — multi-hole

If you finish: **also patch `impl.py`** so it satisfies the spec you just wrote, and add the
tests you proposed. You now hold all four boxes at once. Note in `log.md` anything you discovered
about your own spec by trying to implement against it — that experience is the real deliverable.

---

## 4. Friday — share-out

Bring: your answer to divergence Q1, and the most consequential thing the tests fail to check.

Whole-group: we will run this code twice on the same data with the seed removed, and discuss what
you would have to add before you would put either result in a paper. Then: **what would have to
be true for "four or five cell types" to be an answer rather than an assumption?**

## 5. What you hand in

`design.md` (Monday) · `spec.md` · `notes.md` (divergence + gaps + Depth) · `log.md`
· optionally a patched `impl.py` + new tests

## 6. What we are looking for

| | |
|---|---|
| **Phase 1** | Committed before the gate. Not graded on quality. |
| **Divergence** | Q1 in particular: did you see that the code answers a *narrower* question than the one you were asked? |
| **Spec** | Precise enough to reimplement from. Complete-but-unsurprising is a passing spec, not a strong one. |
| **Gap analysis** | **Weighted most heavily.** Silent-wrong-answer gaps count for more than crash gaps. |

---

## 7. Instructor notes (NOT for students)

### Planted productive uncertainty

1. **`k` is an argument.** The Monday question asks *how many* types; the code cannot answer it and
   the collaborator's "four or five" becomes an unexamined input. This is the **central** planted
   gap and the target of divergence Q1. Nearly everyone should reach it, some only after Q2.
2. **Empty clusters degrade silently — `k` is quietly ignored.** If a centroid takes no members,
   `zip(*[])` yields nothing, so `centroids[c]` becomes `[]`; `dist2` then zips against an empty
   list and returns `0`. **No exception, no failing test.** Verified behavior on a fixture with
   duplicate rows:

   ```
   X = [[0,0,0]]*4 + [[5,6,5],[6,5,6]] + [[20,21,20]],  k=4
   → labels [0,0,0,0,2,2,2]   centroids [[0,0,0], [], [10.3,10.7,10.3], []]
   → 2 clusters actually used out of the 4 requested
   ```

   The observable symptom is **cluster collapse**: you ask for four types, you get two, and
   `within_cluster_ss` still returns a perfectly ordinary number. That is on-message for this week
   in a way a crash would not be — it compounds defect 1.

   **Reachability caveat (authoring requirement).** Because `random.sample` seeds centroids from
   actual data points, empty clusters essentially do not arise on generic continuous data — 200
   random seeds on Gaussian blobs produced none. The trigger is **duplicate or all-zero rows**,
   which is realistic for scRNA-seq (empty droplets, ultra-low-count cells). **The lab fixture
   must therefore contain some all-zero or duplicate rows**, or this defect is unreachable and the
   hint below fires every time.

   *(An earlier draft of this note claimed the empty centroid becomes a "black hole attracting
   every point." That is wrong — `min` breaks the zero-distance tie toward the lowest index, so
   points coincident with a real centroid stay put. The symptom is collapse, not capture.)*

3. **Returned `labels` and `centroids` are one generation out of sync.** `labels` come from the
   assignment step; `centroids` are then recomputed before the loop ends. So the returned pair does
   not describe the same state, and `within_cluster_ss(X, labels, centroids)` — exactly the call
   the tests make — mixes generations. Verified with `n_iter=1`:

   ```
   labels [0,0,0,0,0,1] with centroids [[4.2,4.4],[11.0,10.0]]
   but those centroids imply labels [0,0,0,1,1,1]
   ```

   At convergence it is a fixed point and the discrepancy vanishes, which is why it hides — and it
   interacts with defect 4: when 50 iterations is *not* enough, the returned pair is incoherent.
   Strong students should reach this from the spec-writing task alone, since it is impossible to
   write an honest postcondition for the return value.

4. **No convergence check.** Always exactly 50 iterations — wasteful when converged, silently
   truncating when not.
5. **`random.sample` with no seed inside the function.** Tests seed globally and pass; real use is
   nondeterministic. Feeds the Friday demo.
6. **Squared Euclidean on raw UMI counts** with a 30× library-size range clusters cells largely by
   sequencing depth. The biologically fatal one, and invisible to every test. Bio branch.
7. **`test_ss_decreases_with_more_clusters` has a redundant first call** (`_, c2 = kmeans(...)`
   immediately overwritten) and asserts a property that is true of the *optimum* but not guaranteed
   for this local-search implementation — it can fail on other seeds. Left in deliberately: a
   flaky test that currently passes is exactly what students should learn to distrust.

**Verified against the code as printed** (`n_iter`, seeding, and fixture behavior all run as
described above). Items 1, 4, 5, 6, 7 are reachable by reading; items 2 and 3 need either the right
fixture or the spec-writing task to surface.

### Differences from Week 4 — the term-position contrast

| | Week 4 | Week 10 |
|---|---|---|
| Phase 1 | Pairs | **Individual** |
| S3 | "What properties would it need?" — empty toolbox | **"Actually choose, and justify"** — real menu |
| S4 | 3 failure modes | **4, one of which must be silent-and-plausible** |
| Hand-worked example | Fully worked in the handout | None given |
| Scaffolding | Sub-prompts throughout | Fewer, more open |
| Multi-hole | Not offered | **Offered as an extension** |

That S3 row is the load-bearing one: the "what properties would it need?" framing exists to make
method selection honest in the early weeks when the toolbox holds one item, and it is designed to
mature into genuine selection exactly here.

### Timing

**Monday, last 10 min only:** read the problem aloud ~3, frame S2's parameter-versus-structural-
choice distinction ~5 (it is new this week and the overrun risk if left unexplained), questions ~2.
S1–S4 out-of-class (~30–40 min).

**Wednesday (105 min):** just-in-time teach ~15 (k-means as the hard-assignment limit of a
mixture) · read ~10 · divergence ~25 · spec ~30 · gaps ~20 · wrap ~5. **Depth and the multi-hole
extension are out-of-class** — the extension was never going to fit in the room, which is fine; it
is bait for the fast finishers.

### Risks

- **Defects 2 and 3 are gotcha-adjacent.** Defect 2 is only reachable if the fixture has duplicate
  or all-zero rows (see its caveat above) — check this before running the lab. If the room is dry
  by the 40-minute mark, hint: *"what happens if a cluster ends up with no cells?"* for 2, and
  *"could you write an honest postcondition for what `kmeans` returns?"* for 3. Better a hint than
  the lesson landing as "you missed something unfindable."
- Students may reasonably propose GMM, hierarchical clustering, or PCA-then-cluster in S3. All
  are good answers to the question as posed; **do not treat k-means as the right answer they
  failed to guess.** Week 11 picks these up.
- **This lab's honest conclusion is that the code should not be trusted.** Say so plainly.
  Students accustomed to provided code being correct will find that disorienting, which is the
  intended effect and needs naming rather than hiding.
