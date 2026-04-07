# Input Contract

Use this reference when the request is incomplete, loosely structured, or spread across multiple messages.

## Required Fields

- `subject`: Exact subject name for the SIP entry
- `focus`: Subject focus, competencies, or topic coverage exactly as provided by the user
- `prelim_content`: All user-provided source content for the Prelim term
- `midterms_content`: All user-provided source content for the Midterms term
- `prefinals_content`: All user-provided source content for the Prefinals term
- `finals_content`: All user-provided source content for the Finals term

## Intake Rules

- Accept source material from slides, lecture notes, syllabi, outlines, or other extracted class material only if the user provides it directly.
- Normalize labels only for collection, not for meaning. For example, treat "Midterm" and "Midterms" as the same slot only when the user clearly means the same term.
- Preserve user meaning within each term. Transform wording into formal learning outcomes only when needed.
- Keep all outcomes text-only, even for IT/CS subjects.
- If any required field is missing, ask only for the missing field or fields.
- If the old SIP template file is missing, stop and request it before attempting document creation.
- If source content includes quizzes, exams, or activities, exclude them unless the user explicitly says they must appear in the Learning Outcomes section.

## Minimal Missing-Input Prompt Pattern

Use a short, focused prompt such as:

`I'm missing the Prefinals content and the SIP template file needed to create the Learning Outcomes document exactly as requested. Send those, and I'll generate the final .docx.`
