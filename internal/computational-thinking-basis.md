# Computational Thinking: What BF550 Means By It (INTERNAL)

> **Internal design document — not published** (`internal/` is excluded in `_config.yml`).
> Grounds the course's four design steps in the computational-thinking literature, states where we
> depart from it deliberately, and marks what is ours to develop.
>
> Operational companion: [`course-structure.md`](course-structure.md) §6, which is where the steps
> are actually used.

---

## 1. What we claim, and what we do not

BF550's weekly design stage teaches **computational thinking**: framing a domain question so that a
computation can answer it. We use the term because it names the skill accurately and because it is
already in use elsewhere in the program, so students meet a consistent idea across courses.

We do **not** claim to implement any particular published CT framework, and we do not adopt anyone
else's step names. The four steps below are ours. The literature is used to check them, not to
license them.

This matters because the field's own critics are right that CT is often invoked loosely. Denning
(2017) catalogues the trouble spots — vague definitions, weak measurement, unsubstantiated transfer
claims — and the honest response is to be specific about what we mean rather than to gesture at the
term. §5 states how this course avoids the vagueness he identifies.

## 2. The four design steps

Every problem opens with these, one week before the implementation materials appear.

| | Step | The question students answer | CT correspondence |
|---|---|---|---|
| **D1** | **Frame** | What process produced this data? | Abstraction / modeling — deciding what to represent and what to ignore |
| **D2** | **Decompose** | What has to be computed or estimated? | Decomposition into computable questions |
| **D3** | **Select** | *Early:* what would the right method need to do? *Later:* which method, and why that one? | Algorithm and tool selection |
| **D4** | **Anticipate** | How would it lie to you? | Evaluation, debugging, assessing alternatives |

These replace the earlier `S1`–`S4` placeholders and are **settled**. They are also the four slots
of the model card ([`ml-pedagogy-design.md`](ml-pedagogy-design.md) §4), so exposition and design
share one template.

## 3. The literature we draw on

Verified citations, most useful first for our purposes.

**Weintrop, D., Beheshti, E., Horn, M., Orton, K., Jona, K., Trouille, L., & Wilensky, U. (2016).
Defining Computational Thinking for Mathematics and Science Classrooms.** *Journal of Science
Education and Technology*, 25(1), 127–147.
[doi:10.1007/s10956-015-9581-5](https://link.springer.com/article/10.1007/s10956-015-9581-5)

> **The best fit for this course.** A taxonomy of 22 practices in four categories: *data practices*,
> *modeling and simulation practices*, *computational problem solving practices*, and *systems
> thinking practices*. Two things matter for us. First, it is built for **science** classrooms, so
> it treats modeling as a first-class category rather than a sub-step of problem solving — which is
> exactly the move D1 makes. Second, its computational-problem-solving practices include *preparing
> problems for computational solutions*, *choosing effective computational tools*, *assessing
> different approaches*, and *troubleshooting and debugging* — which is nearly a description of
> D2–D4.

**Rubinstein, A., & Chor, B. (2014). Computational Thinking in Life Science Education.** *PLoS
Computational Biology*, 10(11), e1003897.
[doi:10.1371/journal.pcbi.1003897](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1003897)

> Directly on our domain. Recommends that a course **explicitly reflect on the CT processes
> themselves** rather than leaving them implicit — which is the entire argument for having a named,
> visible design stage instead of letting design happen silently inside implementation. Also argues
> that using existing bioinformatics tools should not displace hands-on work. See §6 for where we
> depart. Extended in Chor & Rubinstein, *Computational Thinking for Life Scientists* (Cambridge,
> 2018).

**Brennan, K., & Resnick, M. (2012). New Frameworks for Studying and Assessing the Development of
Computational Thinking.** *Proceedings of the 2012 Annual Meeting of the American Educational
Research Association*, Vancouver.

> Separates computational **concepts** from **practices** from **perspectives**. The practices —
> testing and debugging, abstracting and modularizing, reusing and remixing — are what BF550 grades.
> Useful as a reminder that **knowing concepts and enacting practices are different things**, and
> that our seats assess the second.

**Grover, S., & Pea, R. (2013). Computational Thinking in K–12: A Review of the State of the
Field.** *Educational Researcher*, 42(1), 38–43.
[doi:10.3102/0013189X12463051](https://journals.sagepub.com/doi/abs/10.3102/0013189x12463051)

> The standard synthesis. Its most relevant conclusion for us is that **assessment is the field's
> weakest point** — which is the opening our divergence analysis walks into (§7).

**Wing, J. M. (2006). Computational Thinking.** *Communications of the ACM*, 49(3), 33–35.
[doi:10.1145/1118178.1118215](https://dl.acm.org/doi/10.1145/1118178.1118215)

> The founding article. Cite for provenance; it is a manifesto rather than a design.

**Denning, P. J. (2017). Remaining Trouble Spots with Computational Thinking.** *Communications of
the ACM*, 60(6), 33–39.

> The necessary counterweight. Read before writing anything that claims CT transfers broadly.

## 4. Where our steps sit in Weintrop's taxonomy

Not a mapping exercise for its own sake — it tells us what we are *not* teaching, which is worth
knowing.

| Weintrop category | BF550 coverage |
|---|---|
| **Modeling & simulation** | **Heavy.** D1 is a modeling step; the probabilistic frame is a modeling commitment; simulation is concentrated in weeks 2–4 and recurs as a Friday diagnostic. |
| **Computational problem solving** | **Heavy.** D2–D4 plus the whole implementation week — preparing problems, choosing tools, assessing approaches, debugging. |
| **Data practices** | **Partial.** Students analyze and visualize real data, but they do not collect or curate it; datasets are provided. A deliberate scope limit, not an oversight. |
| **Systems thinking** | **Light.** Pipelines appear in the compute depth branch and the synthesis project, but thinking-in-levels is not taught explicitly. **The clearest gap** if we later want broader CT coverage. |

## 5. How this course answers the vagueness critique

Denning's central complaint is that CT taught without a computational model degenerates into
generic problem-solving advice. Three features of this course answer it concretely:

1. **Every design terminates in running code.** A design is never assessed in the abstract; it is
   compared against a working implementation with a spec and tests. The computational model is
   never hypothetical.
2. **The steps are domain-specific, not generic.** "What process produced this data?" is a
   bioinformatics question with a right kind of answer, not a content-free heuristic.
3. **We make no transfer claim.** We are not asserting that this improves students' thinking in
   general — only that they get better at framing biological questions computationally, which is
   the thing we actually assess.

## 6. Where we depart from the literature, deliberately

**We start with modeling, not decomposition.** Generic CT opens with "break the problem down."
BF550 opens with "what process produced this data?" You cannot decompose a biological question
sensibly before deciding what you think generated the observations. Weintrop supports treating
modeling as first-class in science settings; the ordering is ours.

**We stage method selection.** The literature treats *choosing effective computational tools* as
one practice. We split it, because in week 3 the toolbox holds one item and "choose a method" is
hollow. Early weeks ask what properties the right method would need; later weeks ask for a choice
with justification. This is driven by a 13-week sequence constraint, not by theory.

**We separate design from authorship — and this is a real tension.** Rubinstein & Chor recommend
programming as a prerequisite and warn that using existing tools should not replace hands-on work.
BF550 makes code *literacy* the primary objective and assumes coding agents.

The honest reconciliation: their concern is that **black-box tool use displaces reasoning**. Our
design stage and divergence analysis are the opposite of black-box — the student does the framing,
decomposition, method selection, and failure analysis, and the agent does the typing. What we
relocate is authorship, not thinking.

But this is a genuine departure from a directly relevant recommendation, and whether it works is an
**empirical question we should treat as one.** If students turn out unable to reason about code
they did not write, the bet failed, and the check-ins and midterm are where that would show up
first.

## 7. What is ours, and open

**Divergence as CT assessment.** Grover & Pea identify assessment as the field's weakest point.
Standard approaches examine what a student *builds* (Brennan & Resnick's artifact-based interviews,
for instance). BF550 instead examines **the gap between a student's design and an expert design of
the same problem** — what they missed, what they caught, and what they can defend as better.

That is arguably a contribution rather than an application: it measures the thing directly ("did
you see what mattered?") rather than inferring it from a finished artifact, and it produces a
written trace that can be compared across a term. **This is worth developing properly and may be
worth writing up** once we have a term of data.

**Open questions we own:**

1. **How far down should decomposition go?** D2 needs a stopping rule students can apply. Candidate:
   *down to the point where each component is a question you could look up a method for.* Untested.
2. **Is the four-step sequence right for a *non*-probabilistic week?** Trees have no generative
   story, so D1 strains. Possibly D1 becomes "what structure in the data would answer this?" for
   those weeks.
3. **Do the steps need to be visible to students by name**, or only as worksheet prompts? Naming
   them supports reflection (Rubinstein & Chor's recommendation); over-naming adds vocabulary.
   Current leaning: name them, use them lightly.
4. **What does a strong D4 look like?** Anticipating failure is the least-taught step anywhere in
   the literature and the most valuable in practice. We have no rubric for it.
