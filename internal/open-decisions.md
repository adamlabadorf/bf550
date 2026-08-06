# Open Decisions (INTERNAL)

> **Internal planning index — not published to the course site.** Tracks the design
> decisions still to be made. Most are also GitHub discussion issues; comment there.
>
> Canonical structure: [`course-structure.md`](course-structure.md). Superseded drafts:
> [`archive/`](archive/).

## Blocking

| Decision | Where it surfaces | Tracking |
|---|---|---|
| **Computational-thinking instrument step names** — BF550 must reuse the program's vocabulary, not invent a parallel set | design-stage template, assignments | blocks the S1–S4 template; awaiting lab consult |
| Finalize biological anchor problems, **written as questions rather than tasks** | schedule | [#1](https://github.com/bu-bioinfo/bf550/issues/1) + author rule 1 |
| Select & provision the student coding agent — **and the textbook tutor, probably the same procurement** | syllabus, /about/ | [#3](https://github.com/bu-bioinfo/bf550/issues/3) |
| Align the 13-week schedule to the Fall calendar | schedule | [#4](https://github.com/bu-bioinfo/bf550/issues/4) |

## Structure & pedagogy

| Decision | Where it surfaces | Tracking |
|---|---|---|
| **How Bayesian?** MLE/MAP + simulation-based uncertainty vs. full posterior/MCMC | lectures (wks 3, 5, 12) | [ml-pedagogy-design §9](ml-pedagogy-design.md#9-deferred-forks) |
| **Simulation's scope** — leaning: front-load wks 2–4 + Friday diagnostic, not a weekly ritual | lectures, Friday sessions | [ml-pedagogy-design §2.1](ml-pedagogy-design.md#21-narrowing-simulation-first) |
| **Topic compression** — merge Clustering I+II; compress t-SNE/UMAP to a demo | schedule | [ml-pedagogy-design §4.1](ml-pedagogy-design.md#41-where-the-content-actually-gets-delivered) |
| **AIAS level for the design stage** — 2 or 1 | assignments, assessment | [course-structure §9](course-structure.md#9-open-and-pending) |
| **Two problems in flight** — fallback is designing every other week (6 not 12) if load proves too high | schedule, assignments | [course-structure §9](course-structure.md#9-open-and-pending) |
| **Decomposition stopping rule** — how far down students decompose | design-stage template | deferred to the team's computational-thinking discussion |
| **Productive uncertainty** — how much per problem, and whether to disclose the policy | assignments | author rule 3; disclosure currently assumed to happen once at term start |
| Divergence-analysis rubric | assessment | [course-structure §7](course-structure.md#7-grading-posture) |
| Is computational thinking assessed anywhere **unaided**? | assessment | check-ins currently cover code reading only |
| Per-week deliverable rubrics and toolchain | assignments | [#5](https://github.com/bu-bioinfo/bf550/issues/5) — bundle now settled ([course-structure §5](course-structure.md#5-what-the-student-actually-has-to-learn)) |

## Textbook & tutor

| Decision | Where it surfaces | Tracking |
|---|---|---|
| **Hosted tutor or bring-your-own?** BYO cannot enforce the seal at all — this may decide procurement | textbook, assignments | [textbook-ai-design §8](textbook-ai-design.md#8-open-questions) |
| Where sealed content lives before its unseal date | textbook repo layout | [textbook-ai-design §8](textbook-ai-design.md#8-open-questions) |
| Is `mode: discover` authorable at scale, or only for the dozen ideas that matter most? | textbook authoring | [textbook-ai-design §8](textbook-ai-design.md#8-open-questions) |
| **Design homogenization** — how to detect it; consider one tutor-free problem as a year-one control | Friday share-out | [textbook-ai-design §6](textbook-ai-design.md#6-risks-in-order-of-seriousness) |

## Course administration

| Decision | Where it surfaces | Tracking |
|---|---|---|
| Synthesis project format (individual/team, scope) | schedule, assessment | [#6](https://github.com/bu-bioinfo/bf550/issues/6) |
| Written midterm logistics | assessment | [#7](https://github.com/bu-bioinfo/bf550/issues/7) |
| BU/program policy statements; program-outcome mapping | syllabus, learning-objectives | [#8](https://github.com/bu-bioinfo/bf550/issues/8) |
| AI attestation wording | syllabus | [#9](https://github.com/bu-bioinfo/bf550/issues/9) |
| Credit-hour expectations | /about/ rationale | [course-design-rationale](course-design-rationale.md) |

## Resolved

| Decision | Outcome |
|---|---|
| ~~Grade weights; final exam vs. synthesis project~~ | ✅ Weights confirmed; project replaces a final exam ([#2](https://github.com/bu-bioinfo/bf550/issues/2)) |
| ~~Fourth exercise seat: Reviewer or Designer~~ | ✅ **Neither.** Design became a universal stage for every problem; three seats remain, and they are labels rather than a rotation |
| ~~Fifth exercise type for story ↔ code~~ | ✅ Moved to the check-in quizzes rather than the lab framework |
| ~~Within-week two-phase lab~~ | ✅ Replaced by the **staggered pipeline** — design problem *N* in week *N*, implement it in week *N+1* ([course-structure §2](course-structure.md#2-why-the-stagger-rather-than-one-lab-per-week)) |
| ~~Method selection degenerate in early weeks~~ | ✅ S3 asks *"what properties would the right method need?"* early, maturing into real selection |
| ~~Where content gets delivered~~ | ✅ Flipped: textbook carries first exposure (~2 hr/week), Monday activates and elaborates, Friday's critique clinic delivers by demonstration |
| ~~Contact format~~ | ✅ **3 × 105-min MWF sessions** (site still says 2 × 75 + lab — see [course-structure §9](course-structure.md#9-open-and-pending)) |

Student-facing pages deliberately omit these notes; they live here and in the issues.
