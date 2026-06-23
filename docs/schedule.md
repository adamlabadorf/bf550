---
title: "Schedule"
permalink: /schedule/
toc: true
toc_sticky: true
---

Each week has **two 75-minute lectures** and **one 1–2 hour lab**. Most weeks include a short
**check-in quiz** (read a code snippet, describe what it does) and a **lab** built on the
[design → spec → test → implementation framework](https://bu-bioinfo.github.io/bf550/assignments/).

The course moves from statistical foundations, through supervised learning and
classification, to the midterm, then into unsupervised learning, clustering, and regression,
and finishes with a synthesis project.

> *Schedule is subject to change. Biological topics and exact week boundaries will be
> finalized before the term begins.*

| Wk | Lecture theme | ML/stats focus | Biological application | Lab type | Check-in |
|---:|---|---|---|:--:|:--:|
| 1 | Course intro & code literacy | What ML is/isn't; design→spec→test→impl; coding agents; AI levels; toolchain setup | Warm-up: GC-content sliding window | A | — |
| 2 | Applied statistics foundations | Distributions, sampling, estimation, hypothesis testing intuition | Count data (RNA-seq counts), multiple testing | A | ✓ |
| 3 | Probability for ML | Bayes' theorem, conditional probability, MLE, Laplace smoothing | k-mer frequencies in sequences | B | ✓ |
| 4 | Classification I: Naive Bayes | Generative classifiers; class priors; likelihood | rRNA read classification | B | ✓ |
| 5 | Classification II & evaluation | Logistic regression, decision boundaries; precision/recall, ROC/AUC, confusion matrices | Variant pathogenicity / gene classification | C | ✓ |
| 6 | Interpretable & tree-based methods | Decision trees, random forests, **feature importance** | Biomarker / feature selection from expression | C | ✓ |
| 7 | Model selection + **midterm** | Bias–variance tradeoff, overfitting, cross-validation; **written code-reading midterm** | (review week) | D | midterm |
| 8 | Dimensionality reduction | PCA; t-SNE / UMAP intuition; when/why to reduce | scRNA-seq embedding & visualization | C | ✓ |
| 9 | Clustering I | k-means, hierarchical clustering; distance metrics | scRNA-seq cell clustering | D | ✓ |
| 10 | Clustering II | Density-based clustering, choosing *k*, cluster validation | Cell-type discovery / marker genes | D | ✓ |
| 11 | Regression & regularization | Linear & regularized regression; generalization | Expression prediction / dosage response | C | ✓ |
| 12 | Choosing a method in practice | Matching algorithm class to problem; pipelines; data leakage; reproducibility | End-to-end mini case (student-chosen) | D | ✓ |
| 13 | Synthesis & frontiers | High-level intro to neural nets/deep learning; limits, ethics, AI in research; project wrap | Synthesis project presentations | — | — |

## What to expect each week

Labs rotate through four exercise types so that, over the term, you practice every part of
code literacy — implementing, testing, specifying, and critiquing. Early labs lean on the
parts that get you oriented; later labs build up to full engineering judgment:

- **Type A — Spec + Tests → Code:** you produce an implementation and account for how it works.
- **Type B — Spec + Code → Tests:** you write tests with hand-calculated expected values.
- **Type C — Code + Tests → Spec:** you read code closely and recover what it's meant to do.
- **Type D — All three → Critique:** you evaluate correctness, efficiency, and design.

See the [assignment framework](https://bu-bioinfo.github.io/bf550/assignments/) for what each
type involves.

## Synthesis project

The course finishes with a project where you produce a complete **design + specification +
tests + implementation** for a real method on a real molecular-biology problem (for example,
a Naive Bayes rRNA classifier or a single-cell RNA-seq clustering pipeline). Every design
decision should have a clear mathematical or biological justification.
