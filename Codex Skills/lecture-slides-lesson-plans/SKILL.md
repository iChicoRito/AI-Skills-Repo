---
name: lecture-slides-lesson-plans
description: Generate reusable lecture slides content and lesson-plan content for semester-based college subjects using a sample PPT as a general structural reference. Use when Codex needs to preserve the lecture hierarchy style, especially `[TITLE/HEADER]` and `[SUB-TITLE/HEADER]`, produce complete weekly lecture content for any week in Prelim, Midterm, Pre-Finals, or Finals, and create the final requested `.md`, `.pdf`, or `.docx` output file when the user specifies a file type, with code snippets included only when the subject requires them.
---

# Lecture Slides And Lesson Plans

Generate lecture content as clean, reusable Markdown text that can be used for lecture slides or lesson plans. After collecting the required inputs, create the actual requested output file in `.md`, `.pdf`, or `.docx` format. Do not create `.pptx` files, visual slide designs, or layout advice.

## Inputs To Collect

Collect or infer these inputs before writing:

- Subject name
- Week label
- Topic or topics for the week
- Scope or coverage for the week
- PPT reference, or the exact phrase `Use the fallback`
- Whether the request is for lecture slides, lesson plan content, or both
- Target file type: `.md`, `.pdf`, or `.docx`

If any item is missing, ask only for the missing item that blocks the work. If the week is omitted but the user names the term and week number in prose, normalize it to `Prelim Week 2`, `Midterm Week 3`, and so on. If the user does not specify the target file type, ask for it before generating the final deliverable.

## Semester Rules

Use this semester structure exactly:

- `Prelim`: Weeks 1-4
- `Midterm`: Weeks 1-4
- `Pre-Finals`: Weeks 1-4
- `Finals`: Weeks 1-4

Treat any teacher-provided sample deck, prior weekly lecture, or approved template as the structural model unless the user says otherwise.

## First Task: Lock The Reference Structure

Before generating the requested week, study the available reference material first.

Choose the structure source in this order:

- A sample deck for the same requested week, if provided
- A sample deck from the same term
- Any approved prior weekly lecture from the same subject
- The fallback template, if no reference deck is available

Extract and preserve as the reusable structural guide:

- The logical order of major sections
- The `[TITLE/HEADER]` pattern
- The `[SUB-TITLE/HEADER]` pattern
- The general placement style used for sections such as `Requirements`
- Any recurring framing text that appears at the start or end of the lecture

Treat the chosen reference as a general model for structure and hierarchy, not as a word-for-word source. Reuse the same logical section flow and heading style for the requested week, but write new content that fits the user's topic and scope.

If the PPT reference is unavailable or unreadable, tell the user to reply with `Use the fallback` so you can draft using the fallback template in [references/weekly-lecture-template.md](references/weekly-lecture-template.md), but mark that the final header wording should be checked against the original reference deck.

## Output Rules

Always begin the lecture content with a short lecture identification block that clearly states:

- `Subject:`
- `Scope:`
- `Week:`
- `Multiple Topics This Week: Yes/No`

After that, generate the complete lecture content as document-ready material and place it into the requested output file.

Follow these rules:

- Build the lecture content in simple text-based Markdown with proper heading levels and bullet hierarchy before converting or saving it to the requested format
- Create the final output as an actual `.md`, `.pdf`, or `.docx` file based on the user's requested file type
- Do not generate `.pptx` files
- Do not output HTML, CSS, JavaScript, JSON, XML, or visual-design instructions
- Keep the structure uniform across the semester
- Use the chosen reference sample's header hierarchy whenever available
- Preserve clear text hierarchy in the final file: title, section headings, subsection headings, body text, and lists must be visually and semantically distinct
- Make the document directly readable without extra cleanup by using proper Markdown headings, spacing, list formatting, and emphasis where needed
- Keep all explanations in lecture-note or lesson-plan form
- Do not discuss slide design, animation, color, icons, or layout aesthetics
- Keep explanations classroom-ready and organized for teaching
- If the subject is programming, IT, or CS related and the topic requires code, include clear and properly formatted code snippets
- If the topic is conceptual or does not require code, do not include code snippets

## Writing Standard

Write like a lecturer preparing class material:

- Use concise but complete teaching points
- Define important terms before examples
- Move from overview to explanation to application
- Keep terminology consistent within the same subject
- Use bullets or short paragraphs that can be pasted into slides
- Use examples that directly support the weekly scope

For all subjects:

- Use clear concept explanations, comparisons, and examples
- Avoid filler text and unnecessary sections
- Only include code when it directly supports the lesson topic and scope

## Lesson Plan Handling

If the user asks for lesson-plan content, keep it text-only in content style and align it with the same weekly lecture scope and structure.

Include only the lesson-plan elements the user requests. If the user does not specify a school format, use a simple structure:

- Topic
- Learning outcomes
- Lecture outline
- Guided discussion points
- Activity or exercise
- Requirements or deliverables
- Recap

## Workflow

1. Read the sample deck, prior lecture, or export.
2. Capture the chosen reference section order and recurring headings.
3. Read the user's new week topic and scope.
4. State the lecture identification block.
5. Rebuild the lecture using the locked reference structure.
6. Create the requested `.md`, `.pdf`, or `.docx` output file containing the final lecture content.
7. Deliver the final result and mention the created file path.
8. Review for consistency, readable document hierarchy, scope alignment, correct file type, and correct code inclusion only when required.

## Template Reference

Use [references/weekly-lecture-template.md](references/weekly-lecture-template.md) as the fallback scaffold and starter format when building the lecture text.
