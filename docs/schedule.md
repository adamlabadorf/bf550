---
title: "Schedule"
permalink: /schedule/
toc: true
toc_sticky: true
---

The course meets **Monday, Wednesday, and Friday for 105 minutes each**. Monday is where we
work with the week's reading; Wednesday is studio; Friday is where we break things. The
[front page]({{ site.baseurl }}/) explains the weekly rhythm in full.

**One thing to know before reading the table: every problem lives for two weeks.** You design
your own approach to it one week, and build against our materials the next. So in any given
week you are *designing* this week's problem and *building* last week's — the build topic
always trails the teaching by one week. That's deliberate: you implement ideas after they've
had a week to settle, not the day you meet them.

## The arc: what is unknown?

The course runs in three acts, organized by a single escalating question — *what is unknown,
and how would you know your answer is right?*

- **Act I — the unknown is a number** (weeks 1–3). Count it, estimate it, put an honest error
  bar on it. *Knowing you're right:* a standard error.
- **Act II — the unknown is an answer you have examples of** (weeks 4–8). Supervised learning:
  generative models, evaluation, discriminative models, regression. *Knowing you're right:*
  held-out data. Closes with the midterm.
- **Act III — nobody gives you the answer** (weeks 9–12). Prediction without a probability
  model, then structure with no labels at all. *Knowing you're right:* there is no ground
  truth — stability, internal validation, and skepticism are all you have. Closes with the
  Act III exam, after which the term belongs to your synthesis project.

> *Schedule is subject to change. Exact dates and check-in weeks will be finalized before the
> term begins.*

## Week by week

| Wk | Act | Monday's topic | You design (this week) | You build (from last week) |
|---:|:--:|---|---|---|
| 1 | I | How this course works; reading code | *Where does the GC content of this genome change — and how do you avoid pointing a collaborator at an artifact?* | — (Wednesday is toolchain setup) |
| 2 | I | Estimation & uncertainty: sampling, error bars, multiple tests | *Are these genes really differentially expressed?* | GC content |
| 3 | I | Bayes' theorem; estimating probabilities from counts | *What species did this sequence come from?* | Differential expression |
| 4 | II | Naive Bayes: classification as a generative story | *Which reads are rRNA, and how confident can you be about any single call?* | Species of origin |
| 5 | II | Evaluation: overfitting, cross-validation, leakage, calibration | *Does the rRNA classifier actually work?* | rRNA classification |
| 6 | II | Logistic regression: modeling the boundary directly | *Is this variant pathogenic?* | Classifier evaluation |
| 7 | II | Linear regression & regularization | *Can expression predict dose response?* | Variant pathogenicity |
| 8 | II | Consolidation + **written midterm** (no AI) | *Given a fresh biological question: choose a method and defend the choice* | Dose–response (light week) |
| 9 | III | Trees & random forests: prediction without the probability story | *Which genes mark treatment response?* | Method selection |
| 10 | III | Dimensionality reduction: PCA (t-SNE/UMAP as demo) | *What structure hides in this expression matrix?* | Biomarkers |
| 11 | III | Clustering: mixture models → k-means; validating *k* | *Do these cells form distinct types — and how many?* | Matrix structure |
| 12 | III | **Act III exam** (Mon, no AI) · frontiers: neural nets as the same machinery, stacked (Fri) | **Your synthesis project** | Cell types |
| 13 | — | Synthesis project studio | — | Your project |

## The two exams

Each act of the course closes with a short, closed-book, **no-AI** code-reading exam — the
same skill the biweekly check-ins rehearse, assessed all at once:

- **Midterm (week 8):** Acts I & II — estimation through regression, the probabilistic family.
- **Act III exam (week 12, Monday):** weeks 9–11 — trees, dimensionality reduction,
  clustering. Week 12's frontiers material is *not* on it.

**There is no exam during finals period.** After the Act III exam on Monday of week 12, the
rest of the term — and your remaining energy — belongs to the synthesis project.

## The synthesis project

The course in miniature, and the culminating assessment: a complete **design → specification
→ tests → implementation** for a real method on a real molecular-biology problem, with every
design decision justified mathematically or biologically. Its design *is* your week-12 design
slot — the same move you'll have made eleven times by then — and weeks 12–13 of studio time
are yours to build it, with instructors and TAs in the room.
