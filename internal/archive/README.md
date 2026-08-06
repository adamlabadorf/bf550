# Archive (INTERNAL)

> Superseded drafts, kept because parts of them remain useful. **Nothing here describes the
> current design.** The current structure is
> [`../course-structure.md`](../course-structure.md).

## `examples-v1/` — the three v1 example labs

Written against the **within-week two-phase structure**: design phase in the last 25–30 minutes of
Monday, materials unsealing in Wednesday's studio, all in one week. That structure was replaced by
the **staggered pipeline** (design problem *N* one week, implement problem *N−1* the next) because
the within-week version gave the design task only minutes, created a brittle cross-day dependency,
and relied on a commitment gate that could not be enforced in its failure case.

**Superseded in these files:** the Monday/Wednesday timings, the "commit before Wednesday"
sequencing, the seat-per-week rotation as a student-tracked thing, and the claim that the whole lab
fits in one week.

**Still valid and worth porting forward:**

| From | What survives |
|---|---|
| [`week-01-lab.md`](examples-v1/week-01-lab.md) | The §0 student-facing explanation of the course machinery; the GC-content problem statement; the **three planted absences** (lowercase, `N`-in-denominator, trailing bases) with verified numbers — `gc_content("gggggggg")` returns `0.0` where it should be `1.0`; the "what my agent decided for me" exercise, which is the single best week-1 idea in any of these drafts |
| [`week-04-lab.md`](examples-v1/week-04-lab.md) | The rRNA problem statement; the k-mer Naive Bayes spec and implementation; the **verified hand-calculation starter** (`2·log 2 ≈ 1.386`, confirmed exact); four planted items including the priors-from-reference-sets flaw |
| [`week-10-lab.md`](examples-v1/week-10-lab.md) | The scRNA-seq problem statement; the k-means implementation with **seven verified planted defects**, including the empty-cluster collapse (needs duplicate/all-zero rows in the fixture) and the labels/centroids generation mismatch |

The productive-uncertainty inventories and their verified reachability notes are the most expensive
content in these files and should be carried into the v2 examples essentially unchanged — the
defects live in the code and problem statements, which the restructuring does not touch.
