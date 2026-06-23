### How these course materials were built

This document describes how the BF550 course site and supporting materials were developed.
It's here because the development process leaned heavily on AI tools, and because this is a
course that explicitly asks students to be transparent about their own AI use — so we hold
the same standard for ourselves. The student-facing short version lives in the
[syllabus](https://bu-bioinfo.github.io/bf550/syllabus/); this is the full disclosure.

### Roles

**The instructor team (Adam Labadorf and co-instructors):** We are the designers, reviewers,
and owners of this course. The pedagogical decisions are ours — the focus on **code literacy
over code authorship**, the **design → spec → test → implementation** assignment framework,
the choice of biological problems, the assessment structure, and the adoption of the
[TILT](https://www.tilthighered.com/resources) and [AIAS](https://aiassessmentscale.com/)
frameworks. We direct the work, review and edit the output, decide what ships, and are
responsible for the final content.

**AI coding agent (Claude, by Anthropic, via Claude Code):** The written materials in this
repo — the Jekyll site pages, syllabus, schedule, learning objectives, assignment framework,
and internal design docs — were **drafted and organized by an AI agent** from our
specifications and direction, in an interactive working session. The agent also built the
site scaffold (mirroring the [BF528](https://bu-bioinfo.github.io/bf528) site), set up this
repository and the planning project board, and filed the open-question issues. We did not
hand-author most of the prose.

### Workflow

1. **Brief.** Adam provided the course concept in detail: the description, the pedagogical
   intent, the credit/contact structure, and the key design choices.
2. **Drafting.** The agent drafted the site and documents and built the Jekyll scaffold from
   that brief and from the
   [bf550-brainstorming](https://github.com/bu-bioinfo/bf550-brainstorming) framework.
3. **Review and iteration.** Adam reviewed the output and directed revisions — for example,
   a dedicated pass to rewrite the copy so it addresses *students* rather than the instructor
   team, and to separate internal planning material from the public site.
4. **Decisions.** What to build, what the course is, and what is acceptable to publish were
   the instructor team's calls throughout.

Working at roughly **AIAS Level 3–4** (AI Collaboration to Full AI): the agent did the
drafting and building; human judgment directed and evaluated it.

### What this means for the materials

* **The pedagogy is intentional.** The teaching philosophy, framework, and assessment design
  were decided by the instructors before and during drafting — they are not artifacts of what
  an AI happened to produce.
* **The copy is a living draft.** These materials are being reviewed and edited by the
  instructor team and will continue to change. Wording is ours to refine; errors are ours to
  fix.
* **Open decisions are tracked openly.** Items still to be settled live in the
  [discussion issues](https://github.com/bu-bioinfo/bf550/issues) and in
  [`internal/open-decisions.md`](internal/open-decisions.md).

### What this means for students

This course treats AI tools as a legitimate, expected part of the work — used deliberately,
verified critically, and disclosed honestly. This document is us doing exactly what we ask of
you: being open about where AI helped, and keeping human judgment accountable for the result.

### Ongoing posture

Norms around AI-assisted course development are still settling. This disclosure will be
updated as the course materials evolve.
