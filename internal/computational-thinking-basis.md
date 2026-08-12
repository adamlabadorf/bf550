# Computational Thinking: What BF550 Means By It (INTERNAL)

> **Internal design document — not published** (`internal/` is excluded in `_config.yml`).
> Grounds the course's four design steps in the computational-thinking literature — foundational
> and current through 2026 — states where we depart from it deliberately, and marks what is ours to
> develop.
>
> Operational companion: [`course-structure.md`](course-structure.md) §6, which is where the steps
> are actually used.

---

## 1. What we claim, and what we do not

BF550's weekly design stage teaches **computational thinking**: framing a domain question so that a
computation can answer it. We use the term because it names the skill accurately and because it is
in use elsewhere in the program, so students meet a consistent idea across courses.

We do **not** claim to implement any particular published CT framework, and we do not adopt anyone
else's step names. The four steps below are ours. The literature is used to check them, not to
license them.

This matters because the field's own critics are right that CT is often invoked loosely. Denning
(2017) catalogues the trouble spots — vague definitions, weak measurement, unsubstantiated transfer
claims — and the honest response is to be specific about what we mean rather than to gesture at the
term. §6 states how this course avoids the vagueness he identifies.

## 2. The four design steps

Every problem opens with these, one week before the implementation materials appear.

| | Step | The question students answer | CT correspondence |
|---|---|---|---|
| **D1** | **Frame** | What process produced this data? | Abstraction / modeling — deciding what to represent and what to ignore |
| **D2** | **Decompose** | What has to be computed or estimated? | Decomposition into computable questions |
| **D3** | **Select** | *Early:* what would the right method need to do? *Later:* which method, and why that one? | Algorithm and tool selection |
| **D4** | **Anticipate** | How would it lie to you? | Evaluation, debugging, assessing alternatives |

These are also the four slots of the model card ([`ml-pedagogy-design.md`](ml-pedagogy-design.md)
§4), so exposition and design share one template.

## 3. Foundational literature

Verified citations, most useful first for our purposes.

**Weintrop, D., Beheshti, E., Horn, M., Orton, K., Jona, K., Trouille, L., & Wilensky, U. (2016).
Defining Computational Thinking for Mathematics and Science Classrooms.** *Journal of Science
Education and Technology*, 25(1), 127–147.
[doi:10.1007/s10956-015-9581-5](https://link.springer.com/article/10.1007/s10956-015-9581-5)

> **Still the best structural fit.** A taxonomy of 22 practices in four categories: *data
> practices*, *modeling and simulation practices*, *computational problem solving practices*, and
> *systems thinking practices*. Built for **science** classrooms, so modeling is first-class rather
> than a sub-step — the move D1 makes. Its problem-solving practices (*preparing problems for
> computational solutions*, *choosing effective computational tools*, *assessing different
> approaches*, *troubleshooting and debugging*) are nearly a description of D2–D4.

**Rubinstein, A., & Chor, B. (2014). Computational Thinking in Life Science Education.** *PLoS
Computational Biology*, 10(11), e1003897.
[doi:10.1371/journal.pcbi.1003897](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003897)

> Directly on our domain. Recommends that a course **explicitly reflect on the CT processes
> themselves** rather than leaving them implicit — the argument for a named, visible design stage.
> See §7 for where we depart. Extended in Chor & Rubinstein, *Computational Thinking for Life
> Scientists* (Cambridge, 2018).

**Brennan, K., & Resnick, M. (2012). New Frameworks for Studying and Assessing the Development of
Computational Thinking.** *AERA Annual Meeting*, Vancouver.

> Separates computational **concepts** from **practices** from **perspectives**. BF550 grades
> practices; the seats assess enactment, not recall.

**Grover, S., & Pea, R. (2013). Computational Thinking in K–12: A Review of the State of the
Field.** *Educational Researcher*, 42(1), 38–43.
[doi:10.3102/0013189X12463051](https://journals.sagepub.com/doi/abs/10.3102/0013189x12463051)

> The standard synthesis; names assessment as the field's weakest point (§8).

**Wing, J. M. (2006). Computational Thinking.** *Communications of the ACM*, 49(3), 33–35 — cite
for provenance. **Denning, P. J. (2017). Remaining Trouble Spots with Computational Thinking.**
*Communications of the ACM*, 60(6), 33–39 — the necessary counterweight; read before claiming
transfer.

## 4. The current literature (2022–2026), and what it changes

A 2025–26 sweep of the field found three developments that bear directly on this course. Net
effect: **the design's central bets have moved from "defensible departure" to "where the field is
heading" — with one sharp empirical warning we must design against.**

### 4.1 CT 2.0: data-driven computational thinking

**Tedre, M. (2022). Computational Thinking 2.0.** Keynote paper, *Proceedings of the 17th Workshop
in Primary and Secondary Computing Education (WiPSCE '22)*.
[doi:10.1145/3556787.3556788](https://dl.acm.org/doi/10.1145/3556787.3556788) (with Denning &
Tedre, *Computational Thinking*, MIT Press, 2019, as the book-length treatment)

> Classical CT ("CT 1.0") is **rule-driven**: solve a problem by defining explicit computational
> steps. Machine learning upends that consensus — in **data-driven** computing ("CT 2.0") the
> program is trained rather than specified, and core CT 1.0 notions (control flow, correctness,
> the notional machine) need rethinking around data, models, and evaluation.
>
> **Consequence for BF550: this course is a CT 2.0 course, and D1 is its signature move.** "What
> process produced this data?" is precisely the question data-driven computing starts from.
> Starting the design steps with modeling rather than decomposition is therefore not a departure
> from CT that needs defending (as §7 once had to argue from Weintrop alone) — it is the ML-era
> form of CT. D4 likewise: when correctness-by-construction is unavailable, *anticipating how the
> model lies* is the CT 2.0 replacement for program verification.

### 4.2 The generative-AI turn in computing education

**Denny, P., Prather, J., Becker, B. A., Finnie-Ansley, J., Hellas, A., Leinonen, J.,
Luxton-Reilly, A., Reeves, B. N., Santos, E. A., & Sarsa, S. (2024). Computing Education in the
Era of Generative AI.** *Communications of the ACM*, 67(2), 56–67.
[doi:10.1145/3624720](https://dl.acm.org/doi/10.1145/3624720)

**ACM Task Force on Generative AI and Programming Assessment, Final Report (February 2026)** —
surveying 750+ educators across 49 countries.
[Report](https://acm-education-genai-task-force.github.io/ACM_Taskforce_GenAI_Report_16Feb26.pdf)

> The mainstream of computing education now recommends, in the face of LLMs that solve typical
> programming exercises: **shift emphasis toward code comprehension, program design, debugging,
> testing, and critical evaluation of AI-generated output**; assess with code review and
> project-based work; keep some assessment secured (no-AI) to measure unaided ability. In the task
> force survey, 69% of educators report that the skills required to create software have changed.
>
> **Consequence for BF550: the course's "deliberate, somewhat controversial bet" is no longer
> controversial — it is close to the field's consensus recommendation.** Code literacy over
> authorship, design/spec/tests as the graded product, No-AI check-ins and midterm alongside
> AIAS-4 studio work: each now has direct backing in the CS-education mainstream. The
> course-design rationale can cite this rather than argue it from first principles.

### 4.3 The empirical warning: the widening gap

**Prather, J., et al. (2024). The Widening Gap: The Benefits and Harms of Generative AI for Novice
Programmers.** *Proceedings of the 2024 ACM Conference on International Computing Education
Research (ICER '24)*.
[doi:10.1145/3632620.3671116](https://dl.acm.org/doi/10.1145/3632620.3671116)

> Observational study of novices programming with GenAI. Students who were already capable used it
> to accelerate work they intended, and could ignore wrong suggestions. **Students who struggled
> had their existing metacognitive difficulties compounded**, acquired new ones, and — the
> damning finding — **finished with an *illusion of competence***: they believed they had performed
> well when they had not.
>
> **Consequence for BF550: this is the precise failure mode of the course's central bet, now with
> evidence.** The population the course most wants to serve — students with the least background —
> is the population GenAI most misleads. The design's existing mechanisms are the right
> countermeasures, and should be understood (and defended, when challenged) as such:
>
> | Mechanism | What it does about the gap |
> |---|---|
> | **No-AI check-ins and midterm** | Pierce the illusion of competence on a regular cadence, before it compounds |
> | **The sealed design stage** | Forces unaided (AIAS-2) thinking *before* the agent can substitute for it |
> | **The divergence analysis** | Makes the student confront, in writing, what they did and did not anticipate |
> | **Hand-calculated test values** | An artifact the agent cannot fake and the student cannot believe they produced if they did not |
> | **"What my agent decided for me"** (week 1) | Teaches the failure mode explicitly, in the first week |
>
> **Added monitoring obligation:** watch the *low-confidence* students' trajectories specifically —
> the gap widens quietly, and course-level averages will hide it. The check-in trend line per
> student is the early-warning instrument we already have.

### 4.4 Broader framings, noted

**Kafai, Y. B., & Proctor, C. (2022). A Revaluation of Computational Thinking in K–12 Education:
Moving Toward Computational Literacies.** *Educational Researcher*, 51(2), 146–151.
[doi:10.3102/0013189X211057904](https://journals.sagepub.com/doi/10.3102/0013189X211057904)

> Distinguishes **cognitive** (skills acquisition), **situated** (identity and participation in
> authentic disciplinary practice), and **critical** (power, ethics, justice) framings of CT.
> BF550 is deliberately cognitive **and** situated — the seats, studio format, and real-data
> problems are participation in disciplinary practice, not skill drills — with the critical framing
> present but light (week 13's limits-and-ethics session; D4's skepticism habit). Recorded so the
> choice is explicit rather than unexamined.

**Hurt, T., Greenwald, E., Allan, S., Cannady, M. A., Krakowski, A., Brodsky, L., Collins, M. A.,
Montgomery, R., & Dorph, R. (2023). The computational thinking for science (CT-S) framework.**
*International Journal of STEM Education*, 10, art. 1.
[doi:10.1186/s40594-022-00391-7](https://link.springer.com/article/10.1186/s40594-022-00391-7)

> Positions CT as an input to and outcome of *science* learning, mediated by computational tools —
> supporting domain-integrated CT (our approach) over standalone CT instruction, and useful for
> distinguishing CT from adjacent skills (mathematical reasoning, generic problem-solving) if we
> are ever asked to.

## 5. Where our steps sit in Weintrop's taxonomy

Unchanged by the recent sweep; kept because it says what we are *not* teaching.

| Weintrop category | BF550 coverage |
|---|---|
| **Modeling & simulation** | **Heavy.** D1; the probabilistic frame; simulation front-loaded in cycles 2–4 and recurring as a Share-session diagnostic. |
| **Computational problem solving** | **Heavy.** D2–D4 plus the implementation week. |
| **Data practices** | **Partial.** Students analyze and visualize real data but do not collect or curate it. A deliberate scope limit. |
| **Systems thinking** | **Light.** Pipelines appear in the synthesis project (and in the deferred compute depth branch). The clearest gap if broader CT coverage is ever wanted. |

## 6. How this course answers the vagueness critique

Denning's central complaint is that CT taught without a computational model degenerates into
generic problem-solving advice. Three concrete answers:

1. **Every design terminates in running code**, compared against a working implementation with a
   spec and tests. The computational model is never hypothetical.
2. **The steps are domain-specific.** "What process produced this data?" is a bioinformatics
   question with a right kind of answer, not a content-free heuristic.
3. **We make no transfer claim.** Only that students get better at framing biological questions
   computationally — the thing we actually assess.

## 7. Where we depart from the literature, deliberately

**We start with modeling, not decomposition.** Generic CT opens with "break the problem down";
BF550 opens with "what process produced this data?" — you cannot decompose a biological question
sensibly before deciding what generated the observations. Weintrop supports modeling as
first-class in science settings, and **Tedre's CT 2.0 makes this the defining move of data-driven
CT** (§4.1). What was once our most exposed choice is now the best-supported one.

**We stage method selection.** The literature treats *choosing effective computational tools* as
one practice. We split it: early weeks ask what properties the right method would need (the
toolbox holds one item); later weeks demand a choice with justification. Driven by the 13-week
sequence, not by theory.

**We separate design from authorship — the real bet.** Rubinstein & Chor recommend programming as
a prerequisite and warn against tools displacing hands-on work. BF550 makes code *literacy* primary
and assumes coding agents. The reconciliation: their concern is black-box use displacing
*reasoning*, and the design stage plus divergence analysis are the opposite of black-box — the
student does the framing, decomposition, selection, and failure analysis; the agent does the
typing. Since 2024 this position has mainstream company (§4.2), **but Prather's widening-gap
finding (§4.3) is the evidence that it can fail for exactly the students it is meant to serve.**
It remains an empirical bet; the check-ins and midterm are where a failed bet shows first, and
per-student check-in trajectories are the early-warning instrument.

## 8. What is ours, and open

**Divergence as CT assessment.** Grover & Pea (2013) named assessment the field's weakest point,
and the recent instrument reviews confirm little has changed: a systematic review of empirical CT
assessment (Tang, X., Yin, Y., Lin, Q., Hadad, R., & Zhai, X. (2020). Assessing computational
thinking: A systematic review of empirical studies. *Computers & Education*, 148, 103798) and a
2024 review of university-context instruments both find the field dominated by **tests and
self-report scales**, with performance-based assessment of authentic practice rare — and nothing
resembling assessment of *design under seal*. BF550 instead examines **the gap between a student's
committed design and an expert design of the same problem**: what they missed, what they caught,
what they can defend as better. It measures the practice directly, produces a written trace
comparable across a term, and — post-GenAI — has the property the ACM task force is asking
assessment to have: it cannot be produced by an agent after the fact, because the commit precedes
the reveal. **Worth developing carefully and plausibly worth writing up after a term of data.**

**Open questions we own:**

1. **Decomposition stopping rule for D2.** Candidate: *down to the point where each component is a
   question you could look up a method for.* Untested.
2. **Does D1 strain on non-probabilistic weeks** (trees)? Likely form there: "what structure in the
   data would answer this?"
3. **Name the steps to students, or keep them as worksheet prompts?** Naming supports reflection
   (Rubinstein & Chor); over-naming adds vocabulary. Leaning: name them, use them lightly.
4. **What does a strong D4 look like?** Still the least-taught step in the literature — nothing in
   the 2022–2026 sweep changes that — and the most valuable in practice. No rubric exists to
   borrow; ours will have to be built from year-one artifacts.
