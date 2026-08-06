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
| Fetch chapter prose on demand, or bundle it in the skill? | textbook skill | [textbook-ai-design §10](textbook-ai-design.md#10-open-questions) |
| How does the tutor know which week it is — infer from chapter, or a date table? | textbook skill | [textbook-ai-design §10](textbook-ai-design.md#10-open-questions) |
| One skill, or a separate notation-decoder skill? | textbook skill | [textbook-ai-design §10](textbook-ai-design.md#10-open-questions) |
| **Authoring order** — the book must exist before the skill is useful, so the skill is realistically a year-two artifact unless a subset of chapters is prioritized | textbook | [textbook-ai-design §10](textbook-ai-design.md#10-open-questions) |
| **Design homogenization** — reduced but not zero; watch in year one, consider a tutor-discouraged control problem | Friday share-out | [textbook-ai-design §8](textbook-ai-design.md#8-residual-risks) |
| No usage visibility with BYO agents — lose the "where is the book unclear" feedback loop | textbook revision | [textbook-ai-design §8](textbook-ai-design.md#8-residual-risks) |
| **Optional MCP server** (stage 6) — decide after a semester of skill use whether telemetry justifies the hosting, uptime, and institutional cost | textbook skill | [textbook-ai-design §4.1](textbook-ai-design.md#41-skill-or-mcp-server) |
| **Ask BU about logging student queries** before building any server that records them; anonymous/aggregate logging likely avoids the issue | textbook skill | [textbook-ai-design §4.1](textbook-ai-design.md#41-skill-or-mcp-server) |

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
| ~~Hosted tutor vs. bring-your-own; sealed textbook content~~ | ✅ **Moot.** The textbook contains **no graded assignments by design**, so there is nothing to seal — the tutor ships as a **Claude skill** students install, and the visibility-tier machinery is deleted ([textbook-ai-design §1](textbook-ai-design.md#1-the-founding-constraint-no-assignments-in-the-textbook)) |

Student-facing pages deliberately omit these notes; they live here and in the issues.
