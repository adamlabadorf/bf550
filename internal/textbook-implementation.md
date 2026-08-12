# Textbook Implementation Plan (INTERNAL)

> **Internal design document — not published.** How the BF550 textbook gets built: toolchain,
> repository layout, chapter anatomy, authoring conventions, CI, and the co-design workflow for
> producing the primary text.
>
> Companions: [`textbook-ai-design.md`](textbook-ai-design.md) (what the book must provide to the
> tutor skill), [`course-structure.md`](course-structure.md) (what the book must provide to the
> course), [`computational-thinking-basis.md`](computational-thinking-basis.md) (the D1–D4 steps
> each chapter's worked design follows).
>
> Prior art: [Biological Data Science in R](https://github.com/bu-bioinfo/biological-data-science-in-r)
> (bookdown → GitHub Pages, executed chunks, `content/` chapters).

---

## 1. Toolchain: Quarto

**Recommendation: Quarto**, executing Python chunks via the Jupyter engine.

| Consideration | Why Quarto |
|---|---|
| **Continuity with bf530** | Quarto is bookdown's successor from the same team (Posit). Same mental model — plain-text chapters, executed chunks, cross-references, one `_quarto.yml` instead of `_bookdown.yml` — so the authoring experience transfers directly. |
| **Python-first** | Chunks execute through Jupyter natively. No `reticulate` shim, no R runtime in the build. |
| **Executed figures** | ` ```{python} ` chunks render figures at build time, exactly as bf530's chunks did. |
| **`freeze: auto`** | Chapter outputs are cached and re-executed only when the chapter source changes. CI stays fast; unchanged chapters are byte-stable. |
| **AI-corpus friendliness** | `.qmd` source is plain markdown with YAML frontmatter — ideal for the skill's reference files, reviewable in diffs, and every heading gets a stable anchor. |
| **Publishing** | Renders to a static site for GitHub Pages, same as bf530. MathJax/KaTeX built in (the notation decoder needs it). |

Considered and passed over: **Jupyter Book** (notebook-native, but `.ipynb` source is hostile to
git diffs, review, and clean corpus extraction; MyST `.md` mode narrows the gap but the ecosystem is
smaller); **bookdown + reticulate** (keeps the exact bf530 tooling but wrong-tools a Python course).

### Execution environment

- **Pinned and lockfiled** (`uv` with `pyproject.toml` + `uv.lock` is the current recommendation;
  conda-lock is the fallback if course tooling standardizes on conda). The book must build
  identically on a laptop and in CI.
- **Every chunk that touches randomness sets an explicit seed.** Non-negotiable — figures are part
  of the text's argument, and an argument that changes between builds is not an argument. (Same
  lesson as author rule 3a: verified behavior, not assumed behavior.)
- Package surface deliberately small: `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `scipy`, and
  as little else as possible. Every additional package is a student-environment liability.

## 2. Repository: its own repo

The textbook lives in a **separate repository** (working name `bf550-textbook`), not in this one.

1. **The safety property is structural.** The tutor-skill design rests on "no graded assignments in
   the corpus." A separate repo makes the boundary physical — the corpus is *the whole repo*, and a
   lab problem cannot drift in without someone noticing the repo it landed in.
2. **It ships as a unit.** The book, the skill, and the optional MCP server are distributed together
   for other adopters ([`textbook-ai-design.md`](textbook-ai-design.md) §4.2). That unit should not
   drag along BF550's internal planning docs.
3. **GitHub Pages mechanics.** This repo's Pages slot is taken by the Jekyll course site; the book
   needs its own.

**Logistics:** the repo needs to be created under the org and added to this session's scope before
scaffolding can start. Until then, all textbook *planning* lives here.

### Layout

```
bf550-textbook/
  _quarto.yml            # book config: chapter order, theme, freeze, MathJax
  pyproject.toml         # pinned environment
  uv.lock
  chapters/
    01-*.qmd … 12-*.qmd  # one chapter per teaching week (see outline)
  appendices/
    notation-decoder.qmd # grows all term; every symbol links back to first use
    toolbox.qmd          # the method menu as it accumulates
  data/                  # small, versioned, real-derived datasets used by chunks
  skill/                 # the tutor skill (SKILL.md + reference/), generated parts marked
  scripts/
    build_corpus.py      # frontmatter → toc.md, concepts.yml, problems.md, llms.txt
    lint_concepts.py     # graph checks (see §5)
  .github/workflows/
    build.yml            # render + execute + lint on every PR; deploy on main
```

## 3. Chapter anatomy

Every chapter has the same skeleton, in the same order. **The order is the pedagogy** — story →
code → notation is enforced by the template, not by author discipline.

```markdown
---
id: naive-bayes            # stable, citable
week: 4
title: "Classifying sequences with Naive Bayes"
concepts: [generative-model, class-prior, likelihood, laplace-smoothing]
prerequisites: [bayes-theorem, mle, kmer-frequencies]
notation_introduced: [posterior-propto, product-notation]
misconceptions:
  - "The independence assumption must hold for the classifier to be useful."
  - "The score a classifier emits is a calibrated probability."
---

## The problem                    <!-- a biological question, phrased as a question -->
## The story                      <!-- generative narrative, prose first -->
## The story, as code             <!-- ~10-30 lines that simulate it; executed, seeded -->
## Playing with the story         <!-- executed chunks; perturb, predict, re-run -->
## Where the numbers come from    <!-- estimation, still in code -->
## The notation                   <!-- the compression, LAST; feeds notation decoder -->
## A worked design                <!-- D1-D4 on an ANALOGOUS problem, not the week's lab -->
## How it lies to you             <!-- assumptions, failure modes; executed demo of one -->
## Practice problems              <!-- ungraded; see §4 -->
```

Three sections earn special comment:

- **The worked design** is the highest-value scaffold in the whole course design
  ([`course-structure.md`](course-structure.md) §6): the student sees a complete D1–D4 pass on a
  problem *adjacent to* the week's design task. Choosing the analogous problem is a real authoring
  decision per chapter — close enough to transfer, far enough not to leak.
- **"How it lies to you"** must contain at least one *executed* failure — a chunk that visibly
  breaks the method by violating its assumption. This is where the simulation-as-diagnostic
  commitment ([`ml-pedagogy-design.md`](ml-pedagogy-design.md) §2.1) lives in the text.
- **The notation section** emits its symbols to the decoder appendix. The decoder is generated, not
  hand-maintained.

## 4. Practice problems and their learning objectives

Ungraded, in-chapter, and the tutor skill needs to know what each is for. Frontmatter per problem:

```yaml
practice_problems:
  - id: p4-2
    kind: predict-the-output        # | modify-the-story | hand-calculate | spot-the-lie | read-the-notation
    objective: >
      Predict how the posterior shifts when the class prior changes,
      before running the code.
    probes: class-prior
    solution: worked                # solutions ARE in the book; they are ungraded
```

**Five problem kinds, recurring in every chapter** so the *shape* of practice is stable while
content varies (the same one-thing-with-a-moving-hole principle as the labs):

| Kind | The move | Serves |
|---|---|---|
| `predict-the-output` | Read code, commit to a prediction, then run | Code literacy; check-in prep |
| `modify-the-story` | Change the generative story; say what changes downstream | D1; the probabilistic frame |
| `hand-calculate` | Tiny instance, worked by hand | Verifier-seat prep |
| `spot-the-lie` | Given output that is subtly wrong, find the violated assumption | D4; critique-clinic prep |
| `read-the-notation` | Translate a formula to prose/code or back | Notation literacy; story↔code check-ins |

Every problem carries an explicit objective sentence. The objective is student-visible — TILT
applies to practice, not only to graded work.

## 5. Generated corpus artifacts and CI

`build_corpus.py` derives the skill's reference files from chapter frontmatter at build time —
**the frontmatter is the single source of truth**; nothing in `skill/reference/` is hand-edited
except `conventions.md`.

| Generated | From |
|---|---|
| `skill/reference/toc.md` | chapter titles, sections, anchors, `week` |
| `skill/reference/concepts.md` + `concepts.yml` | `concepts`, `prerequisites` |
| `skill/reference/problems.md` | `practice_problems` |
| `llms.txt` | all of the above, compact |

**CI on every PR:**

1. **Full render with execution** — every chunk runs; a chapter that does not execute does not merge.
2. **Concept-graph lint** — no cycles; no prerequisite whose `week` is later than its dependent's;
   no concept referenced that is never defined.
3. **Ordering lint** — no display-math block before the chapter's first executed chunk (a cheap,
   imperfect proxy for story → code → notation; authors can override with an explicit marker, and
   the override is visible in review).
4. **Link and anchor check** across chapters and appendices.
5. **Corpus freshness** — generated files match frontmatter (build and diff).

Deploy to Pages on merge to main. `freeze` keeps unchanged chapters' figures byte-identical, which
matters because the skill cites into them.

## 6. Authoring conventions (the style contract)

To be co-designed as its own document in the textbook repo (`CONVENTIONS.md`), but the
non-negotiables are already set by the course design:

1. **Story → code → notation, in that order, every chapter.** The template enforces the skeleton;
   the convention governs within-section writing too — no formula before its simulation.
2. **Voice:** second person, direct, concrete-first — the register of the bf530 book and of the
   course docs. Biological question first in every chapter; the method is the answer, never the
   topic sentence.
3. **Code chunks are read aloud.** Every chunk ≤ ~30 lines, idiomatic but boring Python, no clever
   one-liners — chunks are objects of code literacy, not just figure factories. If a chunk needs a
   comment to be readable, rewrite it until it needs fewer.
4. **Figures follow the dataviz conventions** (one system: consistent palette, direct labeling over
   legends where possible, no unlabeled axes). Every figure is generated by a visible chunk — no
   pasted images of plots.
5. **Every symbol introduced gets a decoder entry** — plain-language gloss plus a code gloss.
6. **Seeds everywhere randomness appears**; datasets small, versioned, and real-derived.
7. **No graded assignment content, ever** — the safety property. Practice problems and their worked
   solutions are the only exercises that live here.

## 7. Content outline: the co-design deliverable

The detailed outline is the next artifact to produce together, one chapter at a time:
**sections → concepts → notation introduced → the worked-design problem → practice problems with
objectives.** Chapter titles below are the frame to fill in, mapped to the course schedule
(clustering merged and t-SNE/UMAP demo-ized, per the settled calendar):

Chapters follow the act structure of the course calendar (`course-structure.md` §4) —
**twelve chapters**, one per teaching week; week 13 introduces no new content.

| Ch | Week | Act | Working title | Worked-design problem (analogous, not the week's problem) |
|---:|---:|:--:|---|---|
| 1 | 1 | I | Questions, computations, and reading code | Reverse complement |
| 2 | 2 | I | Randomness you can run | Coin-flip → read-count sampling |
| 3 | 3 | I | Bayes, counting, and estimation | Codon-usage species classifier |
| 4 | 4 | II | Generative classifiers: Naive Bayes | Promoter-motif presence classifier |
| 5 | 5 | II | Did it actually work? Evaluation & generalization | Evaluating the ch. 3 classifier honestly |
| 6 | 6 | II | Drawing the boundary: logistic regression | Variant effect from conservation scores |
| 7 | 7 | II | Regression, and regularization as a prior | Dosage–response prediction |
| 8 | 8 | II | Choosing a method | Cross-cutting method-selection walkthrough |
| 9 | 9 | III | Trees and forests: the honest outlier | Biomarker panel from expression |
| 10 | 10 | III | Fewer dimensions, same story: PCA | Batch-effect discovery in expression data |
| 11 | 11 | III | Are there groups here? Mixtures, clustering, and validating *k* | Cell-type discovery, GMM → k-means |
| 12 | 12 | III | The same machinery, stacked: a look at neural nets | — (frontiers chapter, lighter; exam-exempt) |

Appendices: **Notation decoder** (generated), **The toolbox** (method menu as it accumulates,
feeding D3), possibly **Python idioms used in this book** (one page, not a Python course).

## 8. Build order

| Stage | Deliverable | Gate |
|---|---|---|
| **0** | This plan agreed; textbook repo created and in session scope | — |
| **1** | Repo scaffold: `_quarto.yml`, environment, CI, `build_corpus.py`, lint, empty chapter shells with frontmatter | CI green on empty book |
| **2** | **One exemplar chapter end-to-end** (ch. 3 or 4 — deep enough to stress every template section) + `CONVENTIONS.md` refined against the experience of writing it | Co-review; conventions frozen |
| **3** | Detailed outline for all chapters (sections, concepts, worked-design problems, practice problems + objectives) | Co-review |
| **4** | Chapters in course order, batched 2–3 per review round | CI + review per batch |
| **5** | Skill assembled from the generated corpus ([`textbook-ai-design.md`](textbook-ai-design.md) §9) | Trigger evals |

Stage 2 before stage 3 is deliberate: **write one real chapter before outlining all of them.** The
exemplar will change the template (it always does), and it is far cheaper to revise one chapter and
an outline than thirteen chapters.

## 9. Open questions

1. **Repo creation and scope** — needs the org repo made and added to the session before stage 1.
2. **`uv` vs conda** for the pinned environment — should match whatever the *course* toolchain
   decision (issue #5 / #3) lands on, so students and book share one environment story.
3. **Worked notebooks** — the course budgets "one chapter + one short worked notebook" per week
   ([`course-structure.md`](course-structure.md) §8). Are notebooks part of this repo (a
   `notebooks/` dir rendered by the same CI) or course-side? Leaning: this repo — they are ungraded
   teaching material, i.e. corpus.
4. **Exemplar chapter choice** — ch. 3 (probability/estimation; stresses simulation + notation) vs
   ch. 4 (Naive Bayes; stresses the full story→code→notation arc plus a worked design). Leaning:
   ch. 4, richest test of the template.
5. **Clustering: one chapter or two** — tracks the topic-compression decision.
