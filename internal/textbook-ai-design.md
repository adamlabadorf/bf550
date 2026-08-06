# The AI-Forward Textbook and Socratic Tutor (INTERNAL)

> **Internal design document — not published** (`internal/` is excluded in `_config.yml`).
> Design for a course textbook that is authored so an LLM can ingest it in a structured way and act
> as a personalized, Socratic tutor.
>
> Companions: [`course-structure.md`](course-structure.md) (the staggered pipeline the textbook has
> to serve), [`ml-pedagogy-design.md`](ml-pedagogy-design.md) (the pedagogy the tutor must obey).
>
> **Status: design sketch.** No implementation decisions made. Prior art for the human-facing form:
> [Biological Data Science in R](https://bu-bioinfo.github.io/biological-data-science-in-r/).

---

## 1. Why this is load-bearing, not a garnish

The tutor is worth building because it is the answer to three problems the course already has, not
because AI tutors are fashionable:

| Existing problem | What the tutor does about it |
|---|---|
| **Wide range of incoming math background** — challenge everyone, leave nobody behind | A tutor meets each student at their own level **without the class visibly tiering.** This is the founding constraint of the course, and a personalized explainer is a better answer to it than anything in the classroom design. |
| **Reading now carries first exposure** (flipped format) — its failure mode is students not reading, or reading without understanding | A tutor that will discuss the chapter with a student converts passive reading into active reading, which is the whole reason flipping works when it works. |
| **Schedule brittleness** — a missed session must be recoverable | Recovery from a tutor that knows what was covered is far better than recovery from a classmate's notes. |

**But it also directly threatens the course's central mechanism**, and that tension shapes the whole
design (§3).

## 2. The hard requirement: the tutor must be able to be blind

BF550's core mechanism is a **sealed design stage** — students commit their own approach to a
problem before seeing ours. A tutor with unrestricted access to the textbook will cheerfully hand a
student the design, and the exercise dies silently. Nobody will notice until the Friday share-out
produces twelve identical answers.

So the textbook needs **visibility tiers baked into its structure**, and the tutor needs to honor
them:

| Tier | Contents | Tutor access |
|---|---|---|
| `open` | Concepts, worked analogous examples, notation, reading chapters | Always |
| `sealed` | Our spec/tests/code for problem *N*; its divergence prompts | **Only after that problem's unseal date** |
| `never` | Planted-uncertainty inventories, instructor notes, rubrics, solutions | Never, under any framing |

This is the requirement that makes the project more than putting a chatbot on the docs, and it is
the one to get right first. A tutor that leaks `never` content is worse than no tutor.

**Note the asymmetry:** the `sealed` tier is time-based and can be enforced by simply not shipping
that content to the tutor's index until the date. The `never` tier is permanent and should live in
**a separate repository or an excluded path** — not merely marked. Content the tutor must never see
should not be in the corpus at all.

## 3. Structuring the content for ingestion

### Per-section frontmatter

Every addressable unit of the textbook carries metadata. A candidate schema:

```yaml
id: laplace-smoothing            # stable, citable anchor
week: 3                          # earliest week this may be discussed
visibility: open                 # open | sealed | never
objective: >
  Estimate a categorical probability from counts without assigning zero
  to an unobserved outcome.
prerequisites: [mle, categorical-distribution, log-probability]
notation_introduced: [alpha, K, p-hat]
mode: discover                   # discover | tell
discover_prompt: >
  What happens to a product of probabilities when one factor is zero?
misconceptions:
  - "Smoothing is a hack rather than a prior."
  - "alpha=1 is optimal rather than conventional."
depth_hooks:
  math: Show that alpha=0 recovers the MLE.
  compute: Why log-space, and where does it matter?
  bio: When is a zero structural rather than unsampled?
```

Four fields are doing the real work:

- **`week`** — stops the tutor spoiling week 9 during week 3, and lets it say *"we get to that
  later; here is what you need for now."* Prevents the most annoying failure mode of a
  whole-corpus tutor.
- **`mode: discover | tell`** — the difference between a tutor and an explainer. `discover` content
  must be reached by questioning, never stated. Without this field, "be Socratic" is a vibe in a
  system prompt that degrades under pressure from a student who just wants the answer.
- **`prerequisites`** — a machine-readable concept graph. Also generates the human textbook's "you
  need this first" links, so it earns its keep twice.
- **`misconceptions`** — gives the tutor something specific to probe for, which is what
  distinguishes a diagnostic question from a generic one.

### Repository-level artifacts

- **`concepts.yml`** — the prerequisite graph, extracted from frontmatter and validated in CI
  (no cycles, no dangling prerequisites, no prerequisite in a later week than its dependent).
  That last check is a genuinely useful lint: it catches curriculum-ordering bugs mechanically.
- **`manifest.json` / `llms.txt`** — the tutor's index: what exists, its tier, its week.
- **Semantic chunking with stable anchors** — every concept independently addressable, so retrieval
  returns a coherent unit rather than a window that straddles two ideas.
- **Tagged code blocks** — each marked with what it demonstrates and whether it is a
  *predict-what-this-does* artifact (in which case the tutor must not simply run it and report).

## 4. Encoding the pedagogy, not just the content

A generic LLM handed a textbook will explain things. Being Socratic, and being *this course's*
tutor, requires the pedagogy to be explicit:

**The story → code → notation rule.** The course's central convention is that ideas arrive as a
story, then as code, then as notation. **The tutor must never lead with the formula**, even when
asked directly — it should offer the story and the simulation first, then the notation as
compression. This is the rule most likely to erode in a long conversation, so it belongs in the
system prompt *and* in per-section metadata.

**Depth escalation is lateral, not vertical.** When a student wants more, the tutor should offer the
math, compute, or bio branch — not "a more advanced version." Encoded in `depth_hooks`.

**Being wrong is safe.** The tutor should treat a wrong answer during design as expected and
productive, and must never imply that a student is behind.

**Notation as a reading skill.** The notation decoder becomes interactive: *"what does this symbol
mean, at my level"* is the single most useful thing a tutor can do for the students who need it
most, and it is exactly what nobody wants to ask out loud in a classroom.

## 5. Tutor modes follow the AIAS levels

The course already labels every stage with an AI level, which maps cleanly onto tutor behavior — so
the tutor's constraints are not a new system for students to learn:

| Course stage | AIAS | Tutor mode | Behavior |
|---|:--:|---|---|
| **Reading / concept study** | — | **Socratic** | Questions before answers; `discover` content stays undisclosed; obeys `week` |
| **Design (week *N*)** | 2 | **Interrogative — strictly** | **May only ask questions.** May not propose a decomposition, name a method, or draft the design. May ask *"what would your output look like?"*; may not answer it. Sealed materials inaccessible. |
| **Week *N+1* work** | 4 | **Full collaborator** | Anything: explain, generate, debug, critique. The graded products (hand-calculated values, divergence analysis, annotation) are ones it cannot supply anyway. |
| **Check-ins, midterm** | 1 | **Off** | Not available. |

The design-stage restriction is the one that matters and the one that will be tested by students. It
is worth stating to them in the same breath as the reason: **the tutor is not withholding help, it
is protecting the only part of the course that cannot be done for you.**

## 6. Risks, in order of seriousness

**1. Design homogenization — the subtle one.** Even a well-gated tutor, consulted by twenty students
about the same problem, may converge their designs. **The Friday share-out depends on designs
differing from each other**, so this could quietly kill the session that makes the depth branches
lateral rather than tiered — and it would look like the students simply agreeing, not like a tool
artifact.

Partial mitigations: hold the design-stage tutor to questions only (§5); make the share-out about
divergence *from the materials* as well as between students; watch for it explicitly in year one.
**Unresolved, and the risk I would monitor most closely.**

**2. Leakage of `never` content.** Mitigated structurally by keeping it out of the corpus rather
than marking it (§2). Any design that relies on the model declining to reveal content it can see is
inadequate.

**3. The tutor doing the productive struggle.** The divergence analysis is worthless if a tutor
wrote it. The AIAS mapping addresses the design stage; week *N+1* is deliberately Level 4, so the
protection there is that the graded artifacts are ones an agent cannot supply — hand-calculated
values, honest accounts of what your own agent decided for you.

**4. Hallucinated biology.** A tutor confidently wrong about a genomic fact, in a course whose
author rule is that answers be verifiable from domain knowledge. Grounding to the corpus with
citations, and explicit instruction to decline rather than extrapolate.

**5. Unobservable usage.** Thousands of tutor conversations, none reviewed. Consider logging with
student consent — both for grading integrity and because *the logs are the best available data on
where the textbook is unclear.* That second use may be the more valuable one.

**6. Equity of access.** If the tutor becomes genuinely load-bearing, it must be provided and
uniform, not BYO-subscription. Ties to [issue #3](https://github.com/bu-bioinfo/bf550/issues/3)
(selecting and provisioning the student coding agent) — probably the same procurement decision.

## 7. Build order

Nothing here requires the full system to be useful, and the sequence is deliberately
lowest-risk-first:

| Stage | Deliverable | Value if we stop here |
|---|---|---|
| **1** | Textbook with frontmatter and stable anchors; `visibility` and `week` populated; `never` content in a separate path | A better human textbook, and a corpus that is safe to point any tool at |
| **2** | `concepts.yml` + CI lint (no cycles, no prerequisite ordered after its dependent) | Catches curriculum-ordering bugs mechanically |
| **3** | Retrieval-grounded tutor honoring `visibility` and `week`, Socratic mode only | The math-range and reading-accountability wins, without touching the design stage |
| **4** | Design-stage interrogative mode | Full AIAS mapping; the risky part, attempted last |
| **5** | Consented logging fed back into revision | The textbook improves where students actually get stuck |

**Stages 1 and 2 are worth doing regardless of whether the tutor is ever built** — they are ordinary
good authoring plus a lint that finds real mistakes. That is the argument for starting there.

## 8. Open questions

1. **Hosted or bring-your-own?** A hosted tutor makes gating enforceable and access equitable but
   costs money and maintenance. A published corpus plus a project instruction file (students use
   their own agent) is nearly free but **cannot enforce the seal at all** — a student can always
   point their own agent at the repository. If the seal only works when hosted, that decides the
   procurement question, and it should be decided before authoring commits to the tier scheme.
2. **Where does sealed content live before its date?** Private repo, separate branch, or release-on-
   schedule? Whatever the answer, the corresponding *human* materials have the same problem, so
   solve both at once.
3. **Is `mode: discover` authorable at scale?** Marking every concept as discover-or-tell, with a
   discovery prompt, is real work on top of writing the prose. Might start with `discover` only for
   the dozen or so ideas where it matters most.
4. **Does the tutor get the model cards?** A tutor that has seen prior-year designs could scaffold
   powerfully — or leak them. Probably `never`, at least in year one.
5. **How is homogenization even measured?** Without a baseline year it is hard to distinguish
   "students converged because of the tutor" from "the problem has one good answer." Consider
   holding one problem tutor-free in year one as a control.
