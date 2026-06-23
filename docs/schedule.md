# 13-Week Schedule (Draft)

Each week: **two 75-minute lectures** + **one 1–2 hour lab**. Most weeks carry a low-stakes
**check-in quiz** (read a code snippet, describe what it does) and a **lab deliverable**
built on the [design → spec → test → implementation framework](assignment-framework.md)
(exercise types A–D).

The arc moves: **statistical foundations → supervised learning & classification →
interpretable / tree-based methods → model selection (midterm) → unsupervised learning &
dimensionality reduction → clustering → regression & regularization → method selection in
practice → synthesis**.

> **DECISION:** biological anchor problems below are *candidates*, not final. Two are
> effectively locked by intent: **rRNA classification w/ Naive Bayes** and **scRNA-seq
> clustering**. The rest are placeholders to be confirmed.
> **GAP:** align week boundaries with the actual Fall academic calendar (breaks, holidays).

| Wk | Lecture theme | ML/stats focus | Biological anchor (candidate) | Lab type | Check-in |
|---:|---|---|---|:--:|:--:|
| 1 | Course intro & code literacy | What ML is/ isn't; design→spec→test→impl; coding agents; AIAS; toolchain setup | Warm-up: GC-content sliding window | A | — |
| 2 | Applied statistics foundations | Distributions, sampling, estimation, hypothesis testing intuition | Count data (RNA-seq counts), multiple testing | A | ✓ |
| 3 | Probability for ML | Bayes' theorem, conditional probability, MLE, Laplace smoothing | k-mer frequencies in sequences | B | ✓ |
| 4 | Classification I: Naive Bayes | Generative classifiers; class priors; likelihood | **rRNA read classification (RDP / Wang 2007)** | B | ✓ |
| 5 | Classification II & evaluation | Logistic regression, decision boundaries; precision/recall, ROC/AUC, confusion matrices | Variant pathogenicity / gene classification | C | ✓ |
| 6 | Interpretable & tree-based methods | Decision trees, random forests, **feature importance** | Biomarker / feature selection from expression | C | ✓ |
| 7 | Model selection + **MIDTERM** | Bias–variance tradeoff, overfitting, cross-validation; **written code-reading midterm** | (review week) | D | midterm |
| 8 | Dimensionality reduction | PCA; t-SNE / UMAP intuition; when/why to reduce | scRNA-seq embedding & visualization | C | ✓ |
| 9 | Clustering I | k-means, hierarchical clustering; distance metrics | **scRNA-seq cell clustering** | D | ✓ |
| 10 | Clustering II | Density-based clustering, choosing *k*, cluster validation | Cell-type discovery / marker genes | D | ✓ |
| 11 | Regression & regularization | Linear & regularized regression; generalization | Expression prediction / dosage response | C | ✓ |
| 12 | Choosing a method in practice | Matching algorithm class to problem; pipelines; data leakage; reproducibility | End-to-end mini case (student-chosen) | D | ✓ |
| 13 | Synthesis & frontiers | High-level intro to neural nets/deep learning; limits, ethics, AI in research; project wrap | **Synthesis project** presentations | — | — |

## Lab-type rotation rationale

The four exercise types are sequenced to build code literacy progressively (see the
[framework doc](assignment-framework.md)):

- **Type A (spec + tests → code)** early — get oriented; lean on agents for implementation.
- **Type B (spec + code → tests)** next — verification, requires real understanding to write
  hand-calculated tests.
- **Type C (code + tests → spec)** mid-course — critical *reading* and spec recovery, the
  core code-literacy skill.
- **Type D (all three → critique)** later — engineering judgment: correctness, efficiency,
  composability.

## Synthesis project

Mirrors the brainstorming repo's Week-4 capstone but as the **course-level project**:
students produce **design + spec + tests + implementation** for a real method on a real
molecular-biology problem (e.g. a Naive Bayes rRNA classifier, or a scRNA-seq clustering
pipeline). Every design decision must have a stated mathematical or biological
justification.

> **GAP:** decide whether the synthesis project is individual or team-based, its scope,
> and whether it replaces a final exam. Decide the candidate project menu.
