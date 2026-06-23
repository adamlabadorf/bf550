# Assessment & AI Policy

## Philosophy

Assessment in BF550 measures the course's actual learning goals: **statistical/ML judgment**
and **code literacy** — not the ability to produce syntax. Because students are *provided
coding agents and expected to use them*, each assessment states an explicit
[AIAS](https://aiassessmentscale.com/) level so AI expectations are unambiguous, and the
graded product is chosen so that AI cannot do the thinking for the student.

## Assessment components

> **DECISION:** weights below are placeholders — confirm the grade breakdown.

| Component | What it measures | AIAS level | Draft weight |
|---|---|:--:|--:|
| Weekly labs (design → spec → test → impl, types A–D) | applied ML + code literacy + agent use | **4** (most) | 35% |
| Weekly check-in quizzes (code reading) | local code comprehension | **1** | 10% |
| Written midterm (code reading) | code comprehension under exam conditions | **1** | 20% |
| Synthesis project (design + spec + tests + impl) | end-to-end judgment on a real problem | **4** | 30% |
| Participation / labs engagement | — | — | 5% |

### Weekly check-in quizzes

Short, low-stakes. Students are given **a provided code snippet and asked to describe what
it does** — behavior, edge cases, and (later in the term) design intent. This is deliberate,
repeated practice for the midterm skill, and a formative signal of who is keeping up.

- **AIAS Level 1 (No AI)** — the whole point is the student's own reading.
- Keep them short (≈10–15 min) and frequent (most weeks).

### Written midterm — code reading

The midterm is a **written, closed-book code-reading exam (AIAS Level 1)**: students read
provided snippets and describe behavior, recover intent, and identify edge cases or bugs —
the same skill the check-ins rehearse, assessed cumulatively.

> **DECISION:** in-class vs. take-home-but-closed-AI; length; whether students may bring a
> language reference sheet.

### Synthesis project

The capstone: produce **design + spec + tests + implementation** for a real method on a real
molecular-biology problem (e.g. Naive Bayes rRNA classifier; scRNA-seq clustering pipeline),
with every design decision justified mathematically or biologically. AIAS Level 4 — agents
welcome; the design, tests, verification, and critique are the student's product.

## AIAS level reference (this course)

| Level | Name | Meaning here |
|------:|------|---|
| 1 | No AI | Closed-book code reading (check-ins, midterm). |
| 2 | AI Planning | AI for brainstorming/outlining only; student develops ideas independently. |
| 3 | AI Collaboration | AI drafts/feedback; student must critically evaluate & modify. |
| 4 | Full AI | Agent generates code throughout; student directs, annotates, verifies, critiques. |
| 5 | AI Exploration | Open-ended creative/co-design use. |

**Default for labs and the project is Level 4.** What protects the learning goal is not
restricting the tool but requiring the **design, specification, hand-calculated tests,
failure log, and critique** — the artifacts an agent cannot author on the student's behalf.

## Integrity in an agent-positive course

- Using a coding agent on a Level-4 task is **expected**, not a violation.
- What *is* a violation: submitting the agent's work as comprehension you don't have —
  e.g. an annotation log that doesn't match the code, hand-calculated test values that
  weren't actually computed, or a critique that misreads the implementation. These surface
  naturally because the deliverables require demonstrated understanding.
- Check-ins and the midterm (Level 1) provide an AI-free baseline of each student's code
  literacy to triangulate against agent-assisted work.

> **GAP:** write the syllabus academic-integrity statement in BU/program-approved language;
> confirm which coding agent is provided and the access/setup students get; define late /
> regrade / accommodation policies.
