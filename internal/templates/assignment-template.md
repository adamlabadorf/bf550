<!--
BF550 assignment template — TILT (Transparent Assignment: Purpose / Task / Criteria).
Copy this file for each problem. Fill every section; delete the HTML comments.

STRUCTURE: each problem spans two cycles (see ../course-structure.md).
  Cycle N   — students design it. Only the PROBLEM STATEMENT is released.
  Cycle N+1 — our materials unseal (in the Build session); students do the
              divergence analysis and produce whichever artifact the strip stars.
Write ONE file per problem covering both cycles; release it in two parts.

Use the strip + seat label. Do not use exercise-type letters.
-->

| | |
|---|---|
| **Problem** | _N_ |
| **Design cycle / Build cycle** | _N_ / _N+1_ |
| **Starred artifact** | _CODE (Implementer) · TESTS (Verifier) · SPEC (Reverse engineer)_ |
| **AIAS level** | _design: 2 (AI Planning) · build: 4 (Full AI)_ |
| **Biological anchor** | _e.g. rRNA classification — phrased as a QUESTION, not a task (author rule 1)_ |
| **Est. time** | _design ~30–40 min out of class; build in studio_ |
| **Due** | _design: before cycle N+1's Build session · build: end of cycle N+1_ |

```
Cycle N       DESIGN      SPEC      TESTS      CODE
             ★ YOURS    ▨ sealed  ▨ sealed   ▨ sealed

Cycle N+1     DESIGN      SPEC      TESTS      CODE
            (committed)   ...       ...        ...        <!-- star the withheld one -->
```

## Purpose  <!-- TILT: WHY -->

- **Why this matters:** _how this connects to research / real practice the student will do._
- **Skills practiced:** _which course [learning objectives](https://bu-bioinfo.github.io/bf550/learning-objectives/) (by
  number) this builds — e.g. code literacy (6–9), verification (11)._
- **How it fits the course:** _what came before, what it sets up._

## Task  <!-- TILT: WHAT -->

_Concrete steps and deliverables. Be explicit. Example for a Reverse-engineer (SPEC) problem:_

1. Read the provided implementation (`impl.py`) and test suite (`test_*.py`).
2. Write `spec.md` describing inputs, outputs, types, and invariants precisely enough to
   re-implement without the code.
3. For **every edge case** the tests cover, explain the design decision behind it.
4. Identify **≥2 behaviors the tests do not cover** and propose tests for them.
5. Summarize ambiguities / underspecified behavior.

**Deliverables (file list):**
- `spec.md`
- gap analysis in `notes.md` _(weighted most heavily for the Reverse-engineer seat)_
- _…plus the artifact your strip stars (`impl.py` + annotation, or `test_*.py`). The process record (failures and what they taught) is a section of `notes.md` — there is no separate log file._

**Allowed tools / AI use:** _state the AIAS level and what it permits here, explicitly._

## Criteria  <!-- TILT: HOW evaluated -->

_Visible-in-advance standard. Use a checklist or rubric table._

| Criterion | Excellent | Acceptable | Not yet |
|---|---|---|---|
| _Spec precision_ | _…_ | _…_ | _…_ |
| _Gap analysis depth_ | _…_ | _…_ | _…_ |
| _Edge-case reasoning_ | _…_ | _…_ | _…_ |
| _Communication / clarity_ | _…_ | _…_ | _…_ |

**Biological-grounding check:** _confirm the correct answer is verifiable from domain
knowledge without running code (required — see assignment-framework.md)._