---
title: "Week 3 — Probability for ML"
---

> **Under construction.** Lecture materials for Week 3 will be posted here.

## Topic

Probability for ML: the probabilistic machinery behind next week's Naive Bayes classifier.
We start with conditional probability and **Bayes' theorem**, which gives the *structure* of a
classifier — posterior ∝ prior × likelihood. We then ask where those probabilities actually
come from: **maximum likelihood estimation (MLE)** turns observed data into probability
estimates, which for sequence data reduces to counting (e.g. estimating a k-mer's probability
as its observed frequency). Finally, **Laplace smoothing** addresses MLE's zero-frequency
problem — an unseen k-mer would get probability 0 and zero out the entire product in Naive
Bayes — by adding a small pseudocount so nothing is treated as strictly impossible. The
biological anchor is k-mer frequencies in sequences, the exact estimates fed into the Week 4
rRNA classifier.

## A closer look: what Laplace smoothing does, and when to use it

Stripped of the k-mer example, the mechanism is this: **you are estimating a probability from
counts, and you nudge every estimate a little toward "uniform/equally likely" by pretending
you saw each possible outcome a few extra times before you started counting.**

$$\hat{p}_i = \frac{n_i + \alpha}{N + \alpha K}$$

- $n_i$ — times you observed outcome $i$
- $N$ — total observations
- $K$ — number of *possible* outcomes
- $\alpha$ — pseudocount (the "imaginary" prior observations; $\alpha=1$ is classic "add-one")

Two practical effects fall out of that formula:

1. **No estimate is ever exactly 0 or exactly 1.** Unseen outcomes get a small floor instead
   of zero — which is what keeps a single unseen k-mer from zeroing out the whole product in
   Naive Bayes.
2. **It pulls estimates toward uniform, most strongly when data is scarce.** With $N=2$
   observations the $+\alpha$ dominates and the estimate sits near $1/K$; with $N=10{,}000$ the
   $+\alpha$ is negligible and you are back to the raw frequency. Smoothing therefore *backs
   off automatically* as evidence accumulates.

That second point is the real generalization: **Laplace smoothing is a regularizer for
probability estimates** — the discrete-count cousin of ridge regression shrinking coefficients
toward zero, except here you shrink probabilities toward the uniform distribution. Formally it
is the **MAP estimate under a Dirichlet/Beta prior**, so "add a pseudocount" literally *is*
"assume a mild prior belief and update it with data."

### When it is appropriate

Reach for it (or some smoothing/prior) whenever **all** of these hold:

| Condition | Why it matters |
|---|---|
| **You're estimating a categorical/multinomial probability from counts** | This is the regime the formula is built for — proportions over a fixed set of outcomes. |
| **Some outcomes are rare or unobserved in your sample** | A fixed vocabulary plus a finite sample is what produces zeros (k-mers, words, rare alleles, sparse contingency tables). |
| **A zero estimate would be wrong or catastrophic downstream** | Multiplying likelihoods (Naive Bayes), taking logs ($\log 0 = -\infty$), or computing ratios (fold-change with a zero denominator) all break on a literal zero. |
| **"Unseen ≠ impossible" is the right assumption** | Absence in *your sample* should mean "rare," not "can't happen." If a zero is genuinely structural — truly impossible, not just unsampled — you should *not* smooth it away. |

### A few practical refinements

- **$\alpha$ is a knob, not a constant.** $\alpha=1$ (add-one) is convention, not optimal.
  Smaller $\alpha$ (≈ 0.01–0.5) smooths more gently and is usually better when $K$ is huge,
  because add-one over a giant vocabulary steals too much probability mass from the events you
  *did* observe. Tune it like any other hyperparameter (cross-validation).
- **It is the simplest member of a family.** When you have structure to exploit, better priors
  exist — backing off to a lower-order distribution (Good–Turing, Kneser–Ney in NLP) or
  hierarchical/empirical-Bayes shrinkage toward a pooled estimate in genomics (e.g. how
  DESeq2/limma stabilize dispersion and fold-change). Laplace is the "always-correct,
  rarely-optimal" baseline.

In one line: **use Laplace smoothing whenever you're turning counts into probabilities, the
outcome space is fixed but sparsely sampled, and a zero would be both statistically
overconfident and operationally harmful — as long as "unobserved" honestly means "rare," not
"impossible."**

## Materials

_To be added._

## Reading / references

_To be added._
