---
link-citations: true
---

> **CURRENTLY UNDER CONSTRUCTION.** This site is being bootstrapped. Content,
> schedule, and policies are drafts — see the planning docs in the
> [GitHub repository](https://github.com/bu-bioinfo/bf550) and the open
> [discussion issues](https://github.com/bu-bioinfo/bf550/issues).

**Semester:** Fall (this year)

**Meeting time:** Two 75-minute lectures + one 1–2 hour lab per week _(days/times TBD)_

**Location:** _TBD_

## Contents

- [Course Objectives](#course-objectives)
- [Course Description](#course-description)
- [What Makes This Course Different](#what-makes-this-course-different)
- [Prerequisites](#prerequisites)
- [Required Software](#required-software)
- [AI Use in This Course](#ai-use-in-this-course)
- [Assessment](#assessment)
- [Course Schedule](#course-schedule)

## Course Objectives

- Build **intuition for the major classes of machine-learning algorithms** —
  supervised vs. unsupervised, classification, clustering, feature-importance /
  tree-based methods, and dimensionality reduction — and learn **how to choose** the
  right method for a biological problem.
- Develop **code literacy**: the ability to *read and understand* code — its behavior,
  its specification, and its design — rather than to author it from scratch.
- Learn to **direct and verify generative-AI coding agents**: decompose a problem into
  design → specification → tests before generating code, then verify that generated code
  does what was intended.
- Apply all of the above to real **molecular-biology and genomics** problems.

See the full [learning objectives]({{ site.baseurl }}/learning-objectives/).

## Course Description

BF550 is an applied introduction to statistics and machine learning for life scientists.
It emphasizes *judgment* — choosing the right method, posing the right problem to a
computational tool, and verifying the answer — over from-scratch programming or
mathematical theory. Work is grounded in real molecular-biology and genomics problems
(e.g. rRNA read classification, single-cell RNA-seq clustering).

## What Makes This Course Different

- **Code literacy over code authorship.** In the age of coding agents, the primary coding
  objective is to *read, specify, test, and critique* code — not to type it from a blank
  page. This levels a classroom with a wide range of incoming programming skill.
- **Coding agents are provided and expected.** Most assignments are
  [AIAS](https://aiassessmentscale.com/) **Level 4**: use the agent freely; your design,
  specifications, tests, and critique are what is graded.
- **Transparent assignments.** Every assignment states its **Purpose, Task, and Criteria**
  up front, following [TILT](https://www.tilthighered.com/resources).

Assignments use a **design → spec → test → implementation** framework with four exercise
types (A–D); see the
[assignment framework]({{ site.baseurl }}/assignments/).

## Prerequisites

Some prior programming experience (any modern language) and introductory
biology/molecular biology. A wide range of programming backgrounds is expected and
explicitly accommodated by the course design.

## Required Software

Students are **provided coding-agent capabilities** _(specific tool TBD)_ and use Python.
Details and setup will be provided in Week 1.

## AI Use in This Course

This course uses the **AI Assessment Scale (AIAS)** (Perkins, Furze, Roe & MacVaugh, 2024)
to make AI policy transparent and consistent. Each component carries an explicit level:

| Level | Name | What it means here |
|---|---|---|
| 1 | **No AI** | Closed-book code-reading (check-in quizzes, written midterm) |
| 2 | **AI Planning** | AI for brainstorming/outlining; ideas developed independently |
| 3 | **AI Collaboration** | AI drafts/feedback; student critically evaluates & modifies |
| 4 | **Full AI** | Agent generates code throughout; student directs, annotates, verifies |
| 5 | **AI Exploration** | Open-ended, co-designed creative use |

Most labs and the synthesis project are **Level 4**. What protects the learning goal is
not restricting the tool but requiring the design, specification, hand-calculated tests,
and critique — the artifacts an agent cannot author on your behalf. Full policy:
[Assessment & AI Policy]({{ site.baseurl }}/assessment/).

## Assessment

There is **no final exam** — the synthesis project is the culminating assessment.

| Component | Measures | AIAS | Weight |
|---|---|:--:|--:|
| Weekly labs (design → spec → test → impl) | applied ML + code literacy + agent use | 4 | 35% |
| Weekly check-in quizzes (code reading) | local code comprehension | 1 | 10% |
| Written midterm (code reading) | code comprehension under exam conditions | 1 | 20% |
| Synthesis project | end-to-end judgment on a real problem | 4 | 30% |
| Participation | — | — | 5% |

## Course Schedule

> *Schedule is subject to change; biological topics and exact dates will be finalized before the term begins.*

| Wk | Lecture theme | ML/stats focus | Biological anchor (candidate) |
|---:|---|---|---|
| [1]({{ site.baseurl }}/lectures/week-01/) | Course intro & code literacy | What ML is/isn't; design→spec→test→impl; agents; AIAS | GC-content sliding window |
| [2]({{ site.baseurl }}/lectures/week-02/) | Applied statistics foundations | Distributions, estimation, hypothesis testing | RNA-seq count data, multiple testing |
| [3]({{ site.baseurl }}/lectures/week-03/) | Probability for ML | Bayes, MLE, Laplace smoothing | k-mer frequencies |
| [4]({{ site.baseurl }}/lectures/week-04/) | Classification I: Naive Bayes | Generative classifiers; priors; likelihood; holding out data to test a model | **rRNA read classification (RDP)** |
| [5]({{ site.baseurl }}/lectures/week-05/) | Evaluation & generalization | Precision/recall, ROC/AUC; overfitting, bias–variance; train/validation/test, cross-validation; data leakage | Evaluating the rRNA classifier honestly |
| [6]({{ site.baseurl }}/lectures/week-06/) | Classification II: logistic regression | Logistic regression, decision boundaries; applying cross-validation & threshold choice | Variant pathogenicity / gene classification |
| [7]({{ site.baseurl }}/lectures/week-07/) | Interpretable & tree-based methods | Decision trees, random forests, feature importance; bias–variance revisited; leakage in feature selection | Biomarker / feature selection |
| [8]({{ site.baseurl }}/lectures/week-08/) | Consolidation + **midterm** | Review of classification & the generalization toolkit | (review week) |
| [9]({{ site.baseurl }}/lectures/week-09/) | Dimensionality reduction | PCA; t-SNE / UMAP intuition; leakage when fitting on all the data | scRNA-seq embedding |
| [10]({{ site.baseurl }}/lectures/week-10/) | Clustering I | k-means, hierarchical; distance metrics | **scRNA-seq cell clustering** |
| [11]({{ site.baseurl }}/lectures/week-11/) | Clustering II | Density-based, choosing *k*, validation without peeking at labels | Cell-type discovery / markers |
| [12]({{ site.baseurl }}/lectures/week-12/) | Regression & regularization | Linear & regularized regression; cross-validation for the regularization path | Expression prediction / dosage |
| [13]({{ site.baseurl }}/lectures/week-13/) | Synthesis & frontiers | Intro to neural nets/DL; limits, ethics | Synthesis project presentations |

