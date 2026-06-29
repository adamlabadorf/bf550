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

## Materials

_To be added._

## Reading / references

_To be added._
