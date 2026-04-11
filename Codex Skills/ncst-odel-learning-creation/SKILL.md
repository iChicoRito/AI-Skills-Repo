---
name: ncst-odel-learning-template
description: >
  Use this skill whenever the user wants to create, fill out, generate, or produce an NCST ODeL Learning Template document. Triggers include: "create a learning template", "fill out the ODeL template", "make a course template", "generate the NCST template for [subject]", "I need the learning template for [course]", or any request to produce structured course documentation following the NCST ODeL format. Also trigger when the user provides course content and asks for it to be organized into the NCST-ODeL structure, even if they don't explicitly say "ODeL" or "template". Always use this skill before producing any NCST course document output.
---

# NCST ODeL Learning Template Skill

This skill generates documents that strictly follow the NCST-ODeL Learning Template structure. It enforces exact section order, complete content, and clean formatting — no added sections, no omissions.

---

## Template Overview

The NCST ODeL Learning Template has exactly **7 required sections** in this fixed order:

1. Course Description
2. Objectives and Expected Outcomes
3. Content Structure and Resources
4. Modality and Strategies
5. Schedule
6. Course Policy
7. References

**All 7 sections must appear. No section may be skipped or reordered. No extra sections may be added.**

---

## General Rules

- Follow the exact section order above — always.
- Use plain text hierarchy only: headings, subheadings, bullet points where appropriate.
- No colors, icons, styling, or decorative formatting.
- Every section must be fully completed — no blank placeholders unless explicitly allowed (see Schedule).
- Content must be self-contained and coherent for the given course.
- Do NOT add sections outside the template.
- Do NOT omit any section.

---

## HARD RULE: Actual Resources Are Required

**Do NOT generate the ODeL template from scratch or from memory.**

All content in the template — topics, objectives, modules, references, policies — must be sourced directly from actual materials uploaded or provided by the user.

If no actual resources are provided, **stop immediately** and ask the user to upload them before proceeding. Do not fabricate, assume, or invent any course content.

---

## Workflow: Before Generating

### Step 0 — Verify Resources Are Present (REQUIRED FIRST STEP)

Before doing anything else, check whether the user has provided actual course materials. Accepted resource types include:

- PowerPoint files (.pptx) — lecture slides, topic outlines
- Word documents (.docx) — syllabus, course guide, module handouts
- PDF files — printed modules, reference materials, course outlines
- Plain text or pasted content — copy-pasted syllabus, topic list, objectives

**If NO resources are provided:**

Stop and respond with this message (adapt tone naturally):

> "Before I can generate the ODeL Learning Template, I need the actual course materials to base it on — such as a PowerPoint, syllabus, module document, or course outline. Please upload or paste your materials and I'll build the template from those."

**Do not proceed until at least one actual resource is provided.**

**If resources ARE provided:**

Read and extract all relevant content from the uploaded files. Use ONLY what is found in those materials. Do not add topics, objectives, or references that are not supported by the provided resources.

---

### Step 1 — Extract Course Information from Resources

From the uploaded materials, extract:

- Course name and code
- Program/department
- Course description or scope (from syllabus or intro slide)
- Topics and modules covered (from slide decks, outlines, or handouts)
- Delivery mode if stated
- Number of weeks or term length if stated
- Any existing policies or grading breakdown
- Any references or cited sources already in the materials

If any of the above are missing from the resources and are required for a section, ask the user specifically for that missing piece — do not invent it.

---

### Step 2 — Check for Schedule Availability

**Before writing Section 5 (Schedule), ask:**

> "Is there an available schedule, or should I generate a placeholder schedule?"

- If the user provides a schedule → use it exactly.
- If no schedule is provided → generate a clearly labeled placeholder with `[Placeholder]` markers and a note: *"Note: This is a placeholder schedule. Replace with actual dates before distribution."*

---

## Section-by-Section Instructions

### Section 1: Course Description

Write a concise 2–4 sentence paragraph that covers:
- What the course is about
- Its scope and coverage
- Its relevance to the program

Do not use bullet points in this section. Write in full paragraph form.

---

### Section 2: Objectives and Expected Outcomes

- Write 3–5 learning objectives.
- Each objective must begin with a measurable action verb (e.g., Identify, Analyze, Demonstrate, Apply, Evaluate).
- Align objectives with program learning outcomes where applicable.
- Format as a numbered or bulleted list.

---

### Section 3: Content Structure and Resources

Organize course topics into weekly or unit-based modules. For each module, include:

- **Module Title**
- **Key Concepts** — list the main topics covered
- **Reading** — textbook chapter, module, or journal article
- **Activity** — type of learning activity (quiz, case study, discussion, etc.)

Format each module consistently. Example:

```
Module 1: [Topic Title]
- Key Concepts: [List]
- Reading: [Source]
- Activity: [Type]
```

Cover all major topics appropriate to the course length and content.

---

### Section 4: Modality and Strategies

Specify:
- Delivery mode: Distance Modular, Online, or Blended
- List of learning activities with estimated time and mode (remote/LMS/synchronous)
- Assessments with estimated time and submission method

Format as a bulleted list. Example:

```
- Delivery Mode: [Online / Distance Modular / Blended]
- Activity: [Description] ([X] hours, [remote/LMS])
- Assessment: [Description] ([X] hours, [LMS/submission method])
- Consultation: [Optional/Required] [platform] session ([X] hour)
```

---

### Section 5: Schedule

Present as a table with these exact columns:

| Week | Topic | Activity | Deadline |

Rules:
- Fill one row per week.
- Match topics to Section 3 modules.
- If no actual schedule is available, use placeholder rows and label the table clearly at the top.
- Deadlines may be labeled `[TBD]` in placeholder mode.

---

### Section 6: Course Policy

Include all of the following sub-items:

- **Submission Deadlines** — due date expectations
- **Late Work Policy** — penalty or grace period details
- **Grading Breakdown** — percentages for each component (must total 100%)
- **Academic Integrity** — brief statement on plagiarism/cheating

Format as a bulleted list. If the user provides specific policies, use them. Otherwise, generate appropriate defaults appropriate to the course type.

---

### Section 7: References

- List all sources that support the course content.
- Use APA format (preferred) or MLA if specified.
- Include at minimum 3 references relevant to the course topics.
- If no references are provided by the user, generate appropriate academic or professional references that match the course subject.
- Format as a plain numbered or bulleted list.

---

## Required Companion Resources

In addition to the `.docx` learning template, the following resources must also be produced or flagged for production:

### PowerPoint Lecture Slides (.pptx)
- Each module in Section 3 requires a corresponding PowerPoint presentation.
- Use the PPTX skill (see `/mnt/skills/public/pptx/SKILL.md`) to generate slides.
- Each slide deck should cover the Key Concepts listed for that module.
- Slide structure per module: Title slide → Learning Objectives → Key Concepts (one per slide) → Summary → End slide.
- Keep slides plain and readable — no excessive animations or decorative themes unless specified.

### Other Resources (if applicable)
Ask the user if any of the following additional materials are needed:
- **Supplementary readings** — PDF or link list per module
- **Assessment sheets** — quiz or activity instruction sheets per module
- **Consultation schedule** — Zoom/Google Meet link and time slots

If the user says yes to any of the above, produce or scaffold them alongside the main template.

---

## Output Format

The final output must:
- Be produced as a `.docx` file using the DOCX skill (see `/mnt/skills/public/docx/SKILL.md`).
- Follow the exact 7-section structure in order.
- Use Heading 1 style for each numbered section title.
- Use Heading 2 or bold text for sub-labels within sections.
- Use the Schedule table from Section 5 as an actual Word table.
- Contain no colors, shading, or decorative elements.
- Be clean, readable, and consistent throughout.

**When producing a `.docx`, always:**
1. Read `/mnt/skills/public/docx/SKILL.md` first.
2. Follow its instructions for creating new documents using `docx-js`.
3. Validate the output before presenting it to the user.

**When producing `.pptx` slides, always:**
1. Read `/mnt/skills/public/pptx/SKILL.md` first.
2. Create one slide deck per module.
3. Validate and present each file to the user.

---

## Quick Checklist Before Submitting Output

- [ ] Actual course resources were uploaded or provided — template was NOT generated from assumptions
- [ ] All content is traceable to the uploaded materials
- [ ] All 7 sections present and in correct order
- [ ] No extra sections added
- [ ] Course Description is a paragraph (not bullets)
- [ ] Objectives use action verbs and came from the actual materials
- [ ] Content Structure reflects topics found in the uploaded resources
- [ ] Modality section lists mode, activities, and assessments
- [ ] Schedule table is complete (or clearly labeled as placeholder)
- [ ] Course Policy includes submission, late work, grading, and integrity
- [ ] References are APA-formatted and sourced from or consistent with provided materials
- [ ] Output is a valid .docx file
- [ ] PowerPoint slide decks created or flagged for each module
- [ ] User asked about additional resources (readings, assessment sheets, consultation schedule)
