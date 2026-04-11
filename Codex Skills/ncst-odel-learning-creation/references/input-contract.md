# Input Contract

Use this reference when the request is incomplete, loosely structured, or spread across multiple messages.

## Required Input

- `course_materials`: Actual uploaded or pasted source materials such as `.pptx`, `.docx`, `.pdf`, syllabus text, module text, or course outline text

## Optional but Important Input

- `course_name_and_code`: Course title and code if present in the source materials
- `program_or_department`: Program or department if present in the source materials
- `delivery_mode`: Online, Distance Modular, or Blended if stated by the user or source materials
- `schedule`: Actual schedule to use for Section 5, if available
- `policies`: Existing submission, late work, grading, or academic integrity rules if provided
- `references`: Existing cited sources or bibliography from the provided materials
- `extra_resources_needed`: Whether the user also wants supplementary readings, assessment sheets, or a consultation schedule

## Intake Rules

- Do not proceed if no actual course materials are provided.
- Use only content supported by the uploaded or pasted materials.
- If required section content is missing from the materials, ask only for the missing piece.
- Ask whether an actual schedule is available before writing Section 5.
- Preserve the exact 7-section NCST ODeL structure in the main skill.
- Do not add course topics, objectives, or references that are not supported by the provided resources.
- Keep the final output plain, structured, and free of decorative formatting.

## Minimal Missing-Input Prompt Pattern

Use a short prompt such as:

`Before I can generate the NCST ODeL Learning Template, I need the actual course materials to base it on. Please upload or paste the syllabus, PowerPoint, module, or course outline.`
