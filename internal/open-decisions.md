# Open Decisions (INTERNAL)

> **Internal planning index — not published to the course site.** Tracks the design
> decisions still to be made. Most are also GitHub discussion issues; comment there.
>
> Canonical structure: [`course-structure.md`](course-structure.md). Superseded drafts:
> [`archive/`](archive/).

## Blocking

| Decision | Where it surfaces | Tracking |
|---|---|---|
| Finalize biological anchor problems, **written as questions rather than tasks** | schedule | [#1](https://github.com/bu-bioinfo/bf550/issues/1) + author rule 1 |
| Select & provision the student coding agent — **and the textbook tutor, probably the same procurement** | syllabus, /about/ | [#3](https://github.com/bu-bioinfo/bf550/issues/3) |
| Align the 13-week schedule to the Fall calendar | schedule | [#4](https://github.com/bu-bioinfo/bf550/issues/4) |

## Structure & pedagogy

| Decision | Where it surfaces | Tracking |
|---|---|---|
| **How Bayesian?** MLE/MAP + simulation-based uncertainty vs. full posterior/MCMC | lectures (wks 3, 5, 12) | [course-structure §9](course-structure.md#9-open-and-pending) |
| **Simulation's scope** — leaning: front-load wks 2–4 + Friday diagnostic, not a weekly ritual | lectures, Friday sessions | [ml-pedagogy-design §2.1](ml-pedagogy-design.md#21-the-scope-of-simulation) |
| **Two problems in flight** — fallback is designing every other week (6 not 12) if load proves too high | schedule, assignments | [course-structure §9](course-structure.md#9-open-and-pending) |
| **Decomposition stopping rule** — how far down D2 should go | design-stage template | [computational-thinking-basis §8](computational-thinking-basis.md#8-what-is-ours-and-open) |
| **Productive uncertainty** — how much per problem, and whether to disclose the policy | assignments | author rule 3; disclosure currently assumed to happen once at term start |
| Divergence-analysis rubric | assessment | [course-structure §7](course-structure.md#7-grading-posture); may be a genuine contribution to CT assessment — [computational-thinking-basis §8](computational-thinking-basis.md#8-what-is-ours-and-open) |
| **What a strong D4 (anticipate failure) looks like** — least-taught step in the literature, no rubric anywhere | assessment | [computational-thinking-basis §8](computational-thinking-basis.md#8-what-is-ours-and-open) |
| Does D1 ("what process produced this data?") strain on non-probabilistic weeks like trees? | design-stage template | [computational-thinking-basis §8](computational-thinking-basis.md#8-what-is-ours-and-open) |
| Is computational thinking assessed anywhere **unaided**? | assessment | check-ins currently cover code reading only |
| **Widening-gap monitoring** — how to track per-student check-in trajectories so struggling students' illusion of competence (Prather et al. 2024) is caught early | assessment, advising | [computational-thinking-basis §4.3](computational-thinking-basis.md#43-the-empirical-warning-the-widening-gap) |
| Per-week deliverable rubrics and toolchain | assignments | [#5](https://github.com/bu-bioinfo/bf550/issues/5) — bundle now settled ([course-structure §5](course-structure.md#5-what-the-student-actually-has-to-learn)) |

## Textbook & tutor

| Decision | Where it surfaces | Tracking |
|---|---|---|
| **Textbook toolchain: Quarto** recommended; environment pinning (`uv` vs conda) should match the course toolchain decision | textbook | [textbook-implementation §1](textbook-implementation.md#1-toolchain-quarto) |
| **Textbook repo** — create `bf550-textbook` under the org and add to session scope | textbook | [textbook-implementation §2](textbook-implementation.md#2-repository-its-own-repo) |
| Worked notebooks — textbook repo or course repo? Leaning: textbook (they are ungraded corpus) | textbook | [textbook-implementation §9](textbook-implementation.md#9-open-questions) |
| Exemplar chapter for stage 2 — ch. 3 or ch. 4? Leaning: ch. 4 | textbook | [textbook-implementation §9](textbook-implementation.md#9-open-questions) |
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
| **Synthesis project: presentation format at 50–60 students** — traditional presentations don't fit; candidates: poster/gallery session, parallel TA-run tracks, recorded lightning talks + structured peer review, written artifact + oral spot-defense sample | schedule, assessment | *(class size is internal-only)* [#6](https://github.com/bu-bioinfo/bf550/issues/6) |
| Synthesis project scope: individual vs. team (team-of-2 would halve presentation and grading volume) | schedule, assessment | [#6](https://github.com/bu-bioinfo/bf550/issues/6) |
| **Agentic grading assistance** — whether/how TAs use agents; needs a policy note before term | assessment | new |
| Written midterm logistics | assessment | [#7](https://github.com/bu-bioinfo/bf550/issues/7) |
| BU/program policy statements; program-outcome mapping | syllabus, learning-objectives | [#8](https://github.com/bu-bioinfo/bf550/issues/8) |
| AI attestation wording | syllabus | [#9](https://github.com/bu-bioinfo/bf550/issues/9) |
| Credit-hour expectations | /about/ rationale | [course-design-rationale](course-design-rationale.md) |

## Settled

| Decision | Outcome |
|---|---|
| The design stage | **Design is a universal stage for every problem**, not a seat. Three seats remain (Implementer, Verifier, Reverse engineer) and are labels rather than a rotation |
| Story ↔ code exercises | Live in the **check-in quizzes**, not the problem framework |
| Design/implement sequencing | **Staggered pipeline** — design problem *N* in week *N*, implement it in week *N+1* ([course-structure §2](course-structure.md#2-why-the-stagger-rather-than-one-lab-per-week)) |
| Design-step names | **D1 Frame · D2 Decompose · D3 Select · D4 Anticipate** — ours, grounded in but not adopted from any published CT framework ([computational-thinking-basis](computational-thinking-basis.md)) |
| Method selection in early weeks | D3 asks *"what properties would the right method need?"* early, maturing into genuine selection as the toolbox fills |
| Where content gets delivered | Flipped: the textbook carries first exposure (~2 hr/week), Monday activates and elaborates, Friday's critique clinic delivers by demonstration |
| Contact format | **3 × 105-min MWF sessions**; front page, schedule, and assessment pages published — remaining pages tracked in [course-structure §9](course-structure.md#9-open-and-pending) |
| Topic sequencing | **Three acts organized by "what is unknown?"** — regression to wk 7, trees to wk 9 post-midterm, clustering one week, t-SNE/UMAP a demo ([course-structure §4](course-structure.md#4-the-pipeline-calendar)) |
| Final assessment | **Act III exam, Monday of week 12** (wks 9–11, no-AI code reading, 15%) + midterm wk 8 (15%); **nothing in finals period** — weeks 12–13 belong to the project. Weights now 30/10/15/15/30/5, superseding [#2](https://github.com/bu-bioinfo/bf550/issues/2) |
| Design-stage AI level | **AIAS 2** (published on the front page as "AI for brainstorming only") |
| Load shedding | Depth = **6 per term** (≥1 per branch, rotational share-outs); `log.md` merged into `notes.md`; graded check-ins biweekly; Monday reading check-in is ungraded telemetry; Friday runs as two blocks; published re-entry rule (missed design → hindsight critique) |
| Tutor delivery & textbook content | The textbook contains **no graded assignments by design**, so nothing needs sealing. The tutor ships as a **portable skill** students install; no visibility tiers ([textbook-ai-design §1](textbook-ai-design.md#1-the-founding-constraint-no-assignments-in-the-textbook)) |

Student-facing pages deliberately omit these notes; they live here and in the issues.
