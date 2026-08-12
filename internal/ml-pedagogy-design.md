# ML Pedagogy — The Probabilistic Frame (INTERNAL)

> **Internal design document — not published to the course site** (`internal/` is excluded in
> `_config.yml`). **This document covers pedagogy only**: how BF550 frames its machine-learning
> content probabilistically, and how it serves a wide range of incoming mathematical background.
>
> **It does not describe course structure.** Weekly format, session budgets, the strip, the seats,
> the deliverable bundle, and the design/implement pipeline all live in
> [`course-structure.md`](course-structure.md).
>
> | Companion | Covers |
> |---|---|
> | [`course-structure.md`](course-structure.md) | **Canonical** week-to-week structure |
> | [`course-design-rationale.md`](course-design-rationale.md) | Why the course makes the code-literacy bet |
> | [`textbook-ai-design.md`](textbook-ai-design.md) | The AI-forward textbook and its tutor skill |
> | [`assignment-framework-authoring.md`](assignment-framework-authoring.md) | Rules for writing problems |
> | [`open-decisions.md`](open-decisions.md) | What is still unsettled |
>
> Deferred decisions bearing on this document are indexed in
> [`open-decisions.md`](open-decisions.md).

---

## 1. The problem this design solves

Students arrive with mathematical backgrounds spanning from very little to a great deal. The
course needs to be **challenging across that whole range without anyone feeling left behind.**
This is the same problem the course already solves for *programming* background via the
code-literacy bet; this document is the equivalent solution for *mathematical* background.

We want a **probabilistic frame** for the ML content — it is the frame that makes the methods
cohere rather than appearing as a bag of tricks — without that frame becoming a mathematical
gate at the door.

### The two reference texts, and what we take from each

| Text | What we take | What we leave |
|---|---|---|
| **Bishop, *Pattern Recognition and Machine Learning*** | The *organizing frame*: methods as probability models; generative vs. discriminative; regularization as a prior; mixtures; latent-variable views | The derivations, the notation density, the assumed calculus/linear algebra |
| **McElreath, *Statistical Rethinking*** | The *delivery method*: minimal notation, intuition first, simulation as the explanatory device, models as stories | The full-Bayesian inference machinery (MCMC/Stan) — see [`open-decisions.md`](open-decisions.md) |

## 2. The key observation about McElreath's method

It is worth being precise about *why* Statistical Rethinking works for readers with modest
math, because the reason is not simply "less math":

> **Simulation replaces derivation as the primary explanatory device.** You state the model as
> a generative story, write the handful of lines that produce fake data from it, then ask what
> could have produced the data you actually observed. Probability becomes counting and running
> things before it becomes algebra.

This fits BF550 unusually well, because **the course's medium is already code.** A generative
story *is* code. So "read the model" and "read the code" become the same act, and the
probabilistic frame reinforces the central code-literacy bet rather than competing with it for
time.

### 2.1 The scope of simulation

Simulation is **not** the primary explanatory device for every method. Making it one would crowd
out the ML content, and it does not generalize: logistic regression and trees have no natural
generative story, and trees are the honest outlier (§5) precisely because there is none to tell.

**Where simulation is load-bearing** (~5 topics): building probability from nothing (wks 2–3), Naive
Bayes, Gaussian mixtures → k-means, probabilistic PCA, regularization-as-a-prior, calibration.

Simulation buys three things, and only the third generalizes:

1. Probability without algebra — **decisive in weeks 2–4**, where the whole point is building
   probabilistic intuition from nothing.
2. Honest treatment of sampling variability — the uncertainty through-line.
3. **Making assumptions visible by violating them and watching the method fail** — this works for
   *every* method, trees included.

Use (3) is a **critique activity, not an exposition activity**. It belongs in the Share session's
critique clinic, not in the Design session's teaching.

> **Simulation is a front-loaded investment plus a recurring diagnostic, not a weekly ritual.**
> Concentrate it in cycles 2–4 where probability is being built; thereafter reach for it in Share sessions
> to break a method by violating its assumptions. Tell the generative story where it is true (NB,
> GMM, PPCA, priors) and do not contort for the rest. This keeps roughly 15 min/week of teaching
> time available in the back half of the term, which is where the ML content is densest.

## 3. Core commitments

### 3.1 Notation literacy *is* code literacy

The course already argues that reading a compressed formal description and saying what it does
is the skill that matters. **We apply that claim verbatim to mathematical notation.** Notation
is not a prerequisite to be gated on; it is a second notation system to become literate in,
taught the way we teach Python — by reading it, not by manipulating it.

This is the single reframe that makes the rest of the design hang together, and it is worth
stating to students explicitly.

### 3.2 The story → code → notation convention

**One public convention we never break: every idea arrives as a story, then as code, then as
notation — in that order.** The formula appears at the *end* of a topic, as the compression of
something students have already simulated and perturbed.

Two payoffs, one for each end of the range:

- **Students with little math** stop experiencing formulas as the gate. By the time
  `p̂ᵢ = (nᵢ + α) / (N + αK)` appears, they have already added pseudocounts in a loop and
  watched the estimate drift toward uniform.
- **Students with a lot of math are not bored**, because *reading and critiquing* a formal
  statement — "what does this expression assume? where does it break?" — is a genuinely
  different skill from deriving it, and most of them have not practiced it.

> **Author rule.** No formula is presented before the simulation it summarizes. If a lecture
> draft leads with notation, it is not finished. `_lectures/week-03.md` currently leads with
> the Laplace-smoothing formula and needs reordering under this rule.

### 3.3 The notation decoder

A single **growing "notation decoder" page**, referenced all term, accumulating symbols as they
appear with a plain-language and a code gloss for each.

**We do not publish a math-prerequisites announcement.** Naming prerequisites sorts students
into "qualified" and "not" before the course starts; an always-available decoder does the same
work without the sorting.

### 3.4 Hard design constraints

Two constraints to hold throughout, because they are what make "no one left behind" real
rather than aspirational:

1. **The core path of every lab is completable without calculus.**
2. **No formula is presented cold** (see 3.2).


## 4. One template, every week

Every method is introduced with the same four slots — **the same four slots as the weekly design
task** (`course-structure.md` §6, grounded in [`computational-thinking-basis.md`](computational-thinking-basis.md)). One artifact, two jobs:

| Slot | As exposition | As a design step |
|---|---|---|
| **The story** | What process would generate data like this? (prose *and* ~10 lines of code) | D1 · Frame |
| **What's unknown** | Which parts of the story are parameters? | D2 · Decompose |
| **How we pin them down** | Counting, optimizing a loss, or a posterior | D3 · Select |
| **How it lies to you** | Assumptions violated, failure modes, what a fooled version looks like | D4 · Anticipate |

Because the design task and the exposition share a template, **the design stage never starts from a
blank page** — it is four prompts, not an empty file.

### When the worksheet becomes a "model card"

The four slots are used **all twelve weeks** as the design worksheet. They earn the name *model
card* only once there is something to estimate:

- **Weeks 1–2** the problems are *computations*, not models — GC content has nothing to estimate,
  so the "what's unknown" slot comes out near-empty. **That emptiness is the lesson**, and it sets
  up the count-versus-estimate distinction that weeks 3–4 depend on. Do not force the card here.
- **From roughly week 3** the slot fills, and the accumulated stack is a genuine model-card set —
  **about ten of them by week 13**, not twelve.

That stack **is** the "intuition for the landscape of ML algorithms" learning objective made
physical, and the obvious scaffold for the synthesis project.

## 5. Probabilistic reframes, week by week

Most of the existing schedule survives intact. These are the weeks where the probabilistic
frame changes the content materially, highest value first:

| Wk | Current topic | Reframe | Why it earns its place |
|---:|---|---|---|
| 11 | Clustering | **k-means as the hard-assignment limit of a Gaussian mixture** | GMM is what makes k-means make *sense* (why spherical? why does it fail on elongated clusters?). EM's intuition — guess assignments, update parameters, repeat — needs zero calculus. Biggest single upgrade available. |
| 4 → 6 | Naive Bayes → logistic regression | **The generative/discriminative pivot**, taught back to back | Naive Bayes literally generates a read from a class; logistic regression models `p(y\|x)` directly. Same problem, two philosophies. PRML 4.1–4.3; the best conceptual moment in the course. |
| 3 | Probability for ML | Add **grid approximation** (Rethinking ch. 2) | Highest-leverage single technique for this audience: a posterior becomes a `for` loop over candidate parameter values, no calculus, and the prior→posterior update is *watchable*. Five lines of readable code unlock the word "posterior" for the term. |
| 7 | Regression & regularization | **Regularization is a prior** — ridge = Gaussian, lasso = Laplace | Closes the week-3 smoothing loop ("add a pseudocount *is* assume a mild prior") four weeks later, adjacent to logistic regression so the linear family is contiguous. |
| 5 | Evaluation | A classifier emits a **distribution**; thresholding is a separate decision-theoretic step (PRML 1.5) | Earns **calibration**, usually skipped, and exactly the right criticism of variant-pathogenicity scores. |
| 10 | Dimensionality reduction | **Probabilistic PCA as the intuition** (latent-variable story), even if computed via SVD | Makes PCA a model with assumptions rather than a rotation recipe. |
| 9 | Trees & forests | The **honest outlier**: what you gain and lose when you drop the probability model | Naming the exception strengthens the frame instead of hiding a gap. Loses calibrated uncertainty; gains interpretability and non-linearity for free. |
| 12 | Neural nets | The same likelihood machinery, stacked | Continuity rather than novelty. |

### The through-line worth naming: uncertainty

The probabilistic frame buys students something specifically biological. In genomics,
essentially every quantity is a noisy estimate from a small sample. The difference between a
student who reports *"my classifier got 0.91 AUC"* and one who reports *"here is the
distribution of AUCs across resamples, and here is why I don't trust the point estimate"* is
the clearest single measure of whether this design worked.

## 6. Differentiation across the background range

**Depth branches — lateral math/compute/bio extensions — are designed but deferred to a future
offering**; the complete design, rationale, and reintroduction checklist are in
[`future-depth-branches.md`](future-depth-branches.md).

Year one's differentiation relies on the mechanisms with no ceiling: the design stage ("how
would it lie to you?" rewards all the sophistication a student brings), the divergence analysis
("where was your design better than ours?"), and the textbook's ungraded practice problems.
Watch the strong tail for boredom — that is the symptom depth branches exist to prevent, and
the trigger for reintroducing them.
