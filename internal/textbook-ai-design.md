# The AI-Forward Textbook (INTERNAL)

> **Internal design document — not published** (`internal/` is excluded in `_config.yml`).
> Design for a course textbook authored so that a coding agent, given a **skill** describing the
> book, can act as a personalized tutor grounded in the actual course materials.
>
> Companions: [`course-structure.md`](course-structure.md) (the staggered pipeline the textbook
> serves), [`ml-pedagogy-design.md`](ml-pedagogy-design.md) (the pedagogy the tutor should reflect).
>
> **Status: design sketch.** Prior art for the
> human-facing form: [Biological Data Science in R](https://bu-bioinfo.github.io/biological-data-science-in-r/).

---

## 1. The founding constraint: no assignments in the textbook

**The textbook contains no graded assignments. By design.** It contains explanation, worked
examples, and **practice problems** — none of which are collected or graded. The labs live
elsewhere (released weekly, per [`course-structure.md`](course-structure.md) §3).

This one decision is what makes the whole thing tractable, and it is worth being explicit about why:

| Problem an AI-readable textbook would normally have | Why it does not arise here |
|---|---|
| The tutor leaks the answers to graded work | **The graded work is not in the corpus.** Nothing to leak. |
| Content must be sealed until a release date | Nothing to seal. A student reading ahead in a *textbook* is a student reading ahead. |
| The seal can only be enforced by a hosted service | No seal, so **bring-your-own-agent is fine** — which is dramatically cheaper and uses tooling students already have |
| Instructor-only material must be excluded from the index | Already solved: it lives in `internal/`, which is excluded from the site |
| Tutor use converges every student's design | Much reduced — the tutor cannot see the design problem at all |

**No visibility tiers, no release gating, no access control.** The structural separation does that
job properly, and any scheme relying on the model declining to reveal content it can see would do it
badly.

## 2. The student story this is built for

> A student is stuck on how a decision tree identifies biomarkers. Earlier in the term they were
> shown how to make their agent aware of the textbook skill. They ask:
>
> *"I'm working through the practice problems in chapter 7 on decision trees and am confused about
> why splitting on one gene at a time can find a combination of markers."*
>
> The agent loads the skill, locates chapter 7, sees which practice problems it contains and what
> each is probing, recognizes the concept and its prerequisites, and guides the student — in this
> course's idiom, citing the sections they should reread.

Everything below is in service of that exchange working well. The design target is not "an AI that
knows machine learning" — the student already has that. It is **an AI that knows *this book*, and
where this student is in it.**

## 3. What the skill has to supply

A generic agent already knows decision trees. Four things it cannot know, in rough order of value:

1. **Where the student is.** Which chapter, which practice problem, what has and has not been
   covered yet. Lets the tutor say *"we get to pruning in chapter 8 — for now the thing to hold is…"*
   instead of dumping the full topic.
2. **What this book says, and in what order.** So the explanation matches the one the student read
   rather than competing with it, and so it can **cite sections back** — see §6.
3. **What each practice problem is for.** A problem probing a specific misconception should be
   guided toward, not solved around.
4. **This course's conventions.** The story → code → notation rule, the design-then-implement
   stagger, the seats, the vocabulary. Cheap to include; makes it feel like this course's
   tutor rather than a chatbot bolted on.

## 4. Architecture

**A skill, not a hosted service.** Students install it once; it works with the agent they already
have. The skill is a map plus a pedagogy note — **not a copy of the book.**

> **Skills are a portable format, not a Claude-specific one.** They are installable across coding
> harnesses via the `skills` CLI (`npx skills …`), so authoring the tutor as a skill does not bind
> the course to a single vendor, and cross-agent portability is therefore not an argument for
> adding an MCP server. *(Confirm the exact install invocation at build time; the portability itself
> is the load-bearing claim.)*

```
bf550-textbook-skill/
  SKILL.md              # map + conventions; the only thing always loaded
  reference/
    toc.md              # chapters, sections, stable anchors, week index
    concepts.md         # concept → defining section, prerequisites, misconceptions
    problems.md         # practice problems → what each one probes
    conventions.md      # course idiom: story→code→notation, the strip, the seats
```

**Progressive disclosure matters here.** `SKILL.md` stays small — what the book is, how it is
organized, when to reach for which reference file, and the handful of pedagogical commitments.
Chapter *content* is fetched from the public site on demand, because the book is already published
as GitHub Pages. Bundling the whole text would bloat the skill and immediately go stale.

**The `description` field is the highest-leverage line in the whole artifact.** It decides whether
the skill fires on *"I'm confused about Gini impurity in chapter 7"* without hijacking unrelated
conversations. It should name the course, the textbook, chapters, and practice problems explicitly.

> When we build this, `skill-creator` (available in Claude Code) handles the scaffolding and has
> tooling for evaluating description-triggering accuracy — which is exactly the thing worth
> measuring.

### 4.1 Skill or MCP server?

They are not alternatives. **A skill carries pedagogy; an MCP server carries capability.** The four
commitments in §6 are behavioral guidance, which is what a skill's markdown is for; tool
descriptions carry that awkwardly at best. An MCP server with no skill would give the agent
excellent data access and no teaching posture.

So the real question is whether the skill needs a **server behind it**.

**What a server would genuinely buy:**

| | Assessment |
|---|---|
| **Server-side logging** | **The real win.** Recovers the "where is the book unclear" feedback loop that BYO agents otherwise cost us (§8 risk 4) — the most valuable textbook-revision data available. |
| **Exact structured answers** | `get_prerequisites("gini-impurity")` returns the graph rather than the agent paraphrasing a markdown table. Modest but real. |
| **Cross-agent portability** | **Not a differentiator.** Skills already install across harnesses via the `skills` CLI (§4). |
| **Semantic search** | **Weaker than it looks.** Thirteen chapters is a small corpus, and in the §2 student story the student *names the chapter*. "Read the TOC, fetch chapter 7" suffices. This solves a problem we do not have. |
| **Executable tools** | **Adds little.** A coding agent already writes and runs Python; a `run_simulation` tool is not a unique capability. |

**What it costs:**

- **It adds a single point of failure the rest of the design avoids.** A skill has no uptime
  requirement. A server must stay up for a semester, and a server down at 11pm before a deadline
  means no tutor. This is the heaviest consideration.
- **Installation friction lands on exactly the wrong students** — configuring an endpoint is more
  than installing a skill, and the students who most need a tutor are the least likely to debug a
  connection error.
- **Logging raises an institutional question, not merely a technical one.** Query logs tied to
  student identity are plausibly educational records; **ask BU before building, not after.**
  Mitigation is straightforward: we want to know *what* was hard, not *who* struggled, so
  **anonymous or aggregate logging captures the whole pedagogical benefit** and sidesteps most of
  the concern.

> **Decision: skill as the floor, server as an optional layer that degrades gracefully.**
>
> **Design constraint to honor from the first commit: the skill must never depend on the server.**
> It navigates by bundled TOC and fetches chapter prose from the public site. If a server exists,
> the skill prefers it for search and it records anonymous queries; if the server is down or was
> never built, everything still works, slightly worse. This is cheap to honor if decided up front
> and expensive to retrofit.
>
> The server therefore becomes **stage 6** of the build order (§9), not a prerequisite — so a
> semester of use decides whether the telemetry justifies hosting, rather than a guess now.

### 4.2 How the server gets deployed and distributed

**Its purpose is logging.** Search and structured queries are secondary; the server exists to answer
*"where is this book unclear?"* Design it around that and resist scope creep.

**Deployment for BF550: an MCP connector scoped to our students.** Because the course provides
Claude subscriptions, the connector can be made available only to enrolled students — which
disposes of two of the cost objections above:

- **Installation friction** largely disappears; a connector provisioned with the subscription is not
  a hand-configured endpoint.
- **Access control** comes free with enrollment, so the server does not need its own auth system —
  which matters, because *not* building auth is what keeps logging anonymous by construction.

**Distribution: the server ships with the textbook.** Anyone adopting the book can deploy their own
instance and get their own telemetry. That makes the textbook a self-contained, reusable artifact
rather than something wired to BU infrastructure, and it means the server must be **configurable,
not hardcoded** — corpus URL, log sink, and retention as configuration.

**Anonymity is a property of the build, not a promise in a privacy policy.** Do not collect
identity. Because access is gated by subscription rather than by in-server auth, there is nothing to
correlate a query against, and the "are these educational records?" question mostly evaporates —
still worth confirming with BU, but from a much better starting position.

**The skill must state all of this plainly**, in language a student reads before their first
question:

> *This course runs an optional server that records the questions asked of this skill — never who
> asked them, and never your conversation. It exists so we can find the parts of the textbook that
> are unclear and fix them. The skill works fully without it.*

Two reasons this belongs in `SKILL.md` rather than only in the syllabus: the student sees it at the
moment of use, and **an agent asked "is this logging me?" should be able to answer accurately from
the skill itself.**

## 5. Metadata, kept light

Per-section frontmatter in the textbook source, from which the reference files are generated:

```yaml
id: gini-impurity
chapter: 7
week: 7
concepts: [impurity, greedy-splitting]
prerequisites: [entropy-intuition, class-proportions]
misconceptions:
  - "A single split must separate the classes; combinations emerge across depth."
  - "Feature importance means causal importance."
practice_problems:
  - id: p7-3
    probes: greedy-splitting
    kind: predict-the-output
```

Four fields earn their keep; the rest is optional:

- **`week`** — lets the tutor calibrate to where the student is, the single most useful thing it can
  know.
- **`prerequisites`** — a concept graph. Also generates the human book's "you need this first" links
  and supports a CI lint (no cycles; no prerequisite scheduled *after* its dependent — that lint
  catches real curriculum-ordering bugs mechanically).
- **`misconceptions`** — what turns a generic question into a diagnostic one. Worth writing for the
  ~20 concepts that matter; skip the rest.
- **`practice_problems.probes`** — so guidance aims at the concept rather than the answer.

**Keep it this light.** A discover-versus-tell mode on every section is not authorable at scale,
and with no sealed content there is nothing for it to protect.

## 6. The pedagogy layer — lightly

Over-specified Socratic instructions degrade badly: they produce an agent that withholds
irritatingly from a student who is genuinely stuck at 11pm the night before a deadline. Four
commitments, stated once in `SKILL.md`:

**Ask one question before explaining, not five.** Find out what the student already thinks. Then
help. A tutor that interrogates is worse than one that explains.

**Never lead with the formula.** The book's central convention is story → code → notation. A tutor
that opens with $$\text{Gini} = 1 - \sum p_i^2$$ has undone the chapter the student just read. Offer
the intuition and the small example first; the notation is the compression at the end.

**Cite sections back into the book.** This is the underrated one. **A good textbook tutor builds
textbook fluency rather than substituting for it** — a student who is repeatedly pointed at §7.3
learns to find §7.3 themselves. It also keeps explanations anchored to what they actually read.

**Escalate laterally, not vertically.** When a student wants more, offer the math, compute, or bio
angle — not "the advanced version." This is the same move the depth branches make in the labs, and
it is the course's core answer to a wide range of incoming background.

### On practice-problem solutions

Do not over-engineer this. **Practice problems are ungraded**, so a student who extracts an answer
has cost themselves some practice and nothing else. Let the solutions be reachable and let the
pedagogy layer encourage working through them. Any scheme that depends on the model *declining* to
reveal content it can see is unreliable anyway.

The graded work is protected structurally, by not being in the corpus.

## 7. Why this is load-bearing

The tutor is worth building because it answers three problems the course already has:

| Existing problem | What the tutor does |
|---|---|
| **Wide range of incoming math background** | Meets each student at their level **without the class visibly tiering.** The founding constraint of the course, and a personalized explainer is a better answer to it than anything available in the classroom. |
| **Reading now carries first exposure** (flipped format) | Converts passive reading into active reading — which is the whole reason flipping works when it works. |
| **Schedule brittleness** | A missed session is recoverable from a book that will discuss itself with you, rather than from a classmate's notes. |

## 8. Residual risks

Short, because §1 removes most of them structurally.

**1. Students paste the assignment into chat.** The tutor cannot see the design problem, but a
student can bring it. This is an AIAS-policy question, not an architecture one — the design stage is
Level 2, and this is exactly what that label is for. It is also self-limiting: the graded artifacts
(hand-calculated values, an honest account of what your own agent decided) are ones the tutor cannot
supply.

**2. Design homogenization** — twenty students consulting the same tutor converging on similar
designs. Substantially reduced now, but not zero, since they can describe the problem themselves.
Worth watching in year one, because it would present as students agreeing rather than as a tool
artifact, and the Share session's share-out depends on designs differing. Consider one tutor-discouraged
problem as a control.

**3. Hallucinated biology.** Mitigated by grounding to the published book and instructing the skill
to cite; the residual is a tutor extrapolating past the corpus. Instruct it to say so.

**4. No visibility into usage.** With bring-your-own agents there are no logs, so we lose the
"conversations show where the book is unclear" feedback loop. That is a real cost of the cheaper
architecture. Partial recovery: have the skill invite students to report sections that needed a lot
of unpacking, and ask for examples in class. **This is the one risk an optional MCP server would
actually retire** (§4.1) — at the price of uptime, installation friction, and an institutional
question about logging.

**5. Equity of access.** If the tutor becomes load-bearing it must be uniformly available. Ties to
[issue #3](https://github.com/bu-bioinfo/bf550/issues/3) — probably the same provisioning decision
as the coding agent, and now cheaper because there is no hosting.

## 9. Build order

| Stage | Deliverable | Value if we stop here |
|---|---|---|
| **1** | Textbook with stable anchors and per-section frontmatter (`week`, `concepts`, `prerequisites`) | A better human book with working prerequisite links |
| **2** | `concepts.md` + CI lint (no cycles; no prerequisite after its dependent) | Catches curriculum-ordering bugs mechanically |
| **3** | `SKILL.md` + `toc.md` + `conventions.md` — a skill that can navigate and cite the book | The student story in §2 works |
| **4** | `misconceptions` on the ~20 concepts that matter; `problems.md` | Guidance becomes diagnostic rather than generic |
| **5** | Trigger evals + a handful of scripted student questions as regression tests | The skill can be *versioned and tested* — a real advantage over an ad-hoc chatbot |
| **6** *(optional)* | MCP server: search, exact graph queries, **anonymous** query logging. Skill prefers it when present, works without it (§4.1) | Recovers the textbook-revision feedback loop — **only worth it if a semester of use shows the telemetry matters** |

Stages 1 and 2 are ordinary good authoring plus a lint that finds real mistakes. **They are worth
doing whether or not the skill ships**, which is the argument for starting there.

## 10. Open questions

1. **Fetch or bundle the chapter text?** Fetching keeps the skill small and current but assumes
   network access and a fetch-capable agent. Bundling works offline but goes stale and is large.
   Hybrid — bundle the index, fetch the prose — is the current leaning.
2. **How does the tutor know which week it is?** Inferring from the chapter the student names is
   probably enough, with a fallback question. A date-to-week table in the skill would be more
   precise but needs updating each offering.
3. **One skill or several?** A single textbook skill is simplest. A separate one for the notation
   decoder — *"what does this symbol mean, at my level"* — might trigger more reliably for the
   students who most need it and are least likely to ask in class.
4. **How much course-structure vocabulary belongs in `conventions.md`?** Enough that the tutor
   understands "I'm the Verifier this week," without drifting into helping with the lab.
5. **Does the skill get the worked designs from the textbook?** The scaffolding ladder
   (`course-structure.md` §6) puts a worked design for an *analogous* problem in each chapter. Those
   are textbook content, so the tutor sees them — which is probably good, and is the main way it can
   support the design stage without touching the actual assignment.
6. **Authoring order versus the course itself.** The book has to exist before the skill is useful,
   and the first offering is when the book gets written. Realistically the skill is a year-two
   artifact unless a subset of chapters is prioritized.
