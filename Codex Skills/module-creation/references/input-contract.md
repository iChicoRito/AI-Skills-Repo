# Input Contract

Use this reference when the request is incomplete, loosely structured, or spread across multiple messages.

## Required Fields

- `subject`: Exact subject name for the module
- `focus`: Subject focus, coverage, or topic list exactly as provided by the user
- `prelim_content`: All user-provided content for the Prelim term
- `midterms_content`: All user-provided content for the Midterms term
- `prefinals_content`: All user-provided content for the Prefinals term
- `finals_content`: All user-provided content for the Finals term

## Intake Rules

- Normalize labels only for collection, not for meaning. For example, treat "Midterm" and "Midterms" as the same slot only if the user clearly means the same term.
- Preserve user wording and sequencing within each term unless the template forces a formatting change.
- If any required field is missing, ask only for the missing field or fields.
- If the user provides content that looks like tests, quizzes, or activities, keep it out unless the user explicitly says it belongs in the module and the template supports it.
- If the subject is not clearly IT/CS-related, default to discussion-only content with no code snippets.
- If the template file is missing, stop and request the template before proceeding with document creation.

## Minimal Missing-Input Prompt Pattern

Use a short, focused prompt such as:

`I'm missing the Midterms content and the template file needed to create the module exactly as requested. Send those, and I'll generate the final .docx.`
