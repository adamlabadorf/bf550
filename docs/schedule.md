---
title: "Schedule"
permalink: /schedule/
toc: true
toc_sticky: true
---

Each week has **two 75-minute lectures** and **one 1–2 hour lab**. Most weeks include a short
**check-in quiz** (read a code snippet, describe what it does) and a **lab** built on the
[design → spec → test → implementation framework](https://bu-bioinfo.github.io/bf550/assignments/).

The course builds from statistical foundations to a first realistic classifier (Naive
Bayes), then immediately establishes the core of honest machine learning — overfitting and
the bias–variance tradeoff, train/validation/test splits, cross-validation, data leakage,
and model selection. Those ideas are introduced early and then recur as a light running
theme through the rest of the supervised methods, unsupervised learning, clustering, and
regression, before the course finishes with a synthesis project.

> *Schedule is subject to change. Biological topics and exact week boundaries will be
> finalized before the term begins.*

| Wk | Lecture theme | ML/stats focus | Biological application | Lab type | Check-in |
|---:|---|---|---|:--:|:--:|
| 1 | Course intro & code literacy | What ML is/isn't; design→spec→test→impl; coding agents; AI levels; toolchain setup | Warm-up: GC-content sliding window | A | — |
| 2 | Applied statistics foundations | Distributions, sampling, estimation, hypothesis testing intuition | Count data (RNA-seq counts), multiple testing | A | ✓ |
| 3 | Probability for ML | Bayes' theorem, conditional probability, MLE, Laplace smoothing | k-mer frequencies in sequences | B | ✓ |
| 4 | Classification I: Naive Bayes | Generative classifiers; class priors; likelihood; **holding out data to test a model** | rRNA read classification | B | ✓ |
| 5 | Evaluation & generalization | Precision/recall, ROC/AUC, confusion matrices; **overfitting/underfitting, bias–variance; train/validation/test splits; cross-validation; data leakage** | Evaluating the rRNA classifier honestly | C | ✓ |
| 6 | Classification II: logistic regression | Logistic regression, decision boundaries; *applying* cross-validation & threshold choice | Variant pathogenicity / gene classification | C | ✓ |
| 7 | Interpretable & tree-based methods | Decision trees, random forests, **feature importance**; bias–variance *revisited* via tree depth; leakage in feature selection | Biomarker / feature selection from expression | D | ✓ |
| 8 | Consolidation + **midterm** | Review of classification & the generalization toolkit; **written code-reading midterm** | (review week) | D | midterm |
| 9 | Dimensionality reduction | PCA; t-SNE / UMAP intuition; when/why to reduce; leakage when fitting on all the data | scRNA-seq embedding & visualization | C | ✓ |
| 10 | Clustering I | k-means, hierarchical clustering; distance metrics | scRNA-seq cell clustering | D | ✓ |
| 11 | Clustering II | Density-based clustering, choosing *k*, cluster validation without peeking at labels | Cell-type discovery / marker genes | D | ✓ |
| 12 | Regression & regularization | Linear & regularized regression; cross-validation for the regularization path — model selection revisited | Expression prediction / dosage response | C | ✓ |
| 13 | Synthesis & frontiers | High-level intro to neural nets/deep learning; limits, ethics, AI in research; project wrap | Synthesis project presentations | — | — |

> **A recurring theme, not a one-time topic.** Overfitting, cross-validation, data leakage,
> and model selection apply to *every* method we cover, so they are introduced early (week 5)
> rather than saved for the end, and then revisited whenever a new method gives us a fresh way
> to get them wrong. Expect them to show up lightly throughout the term — woven into labs and
> check-ins — rather than as a rigid per-week rubric.

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
