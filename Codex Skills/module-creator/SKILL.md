---
name: module-creator
description: Create strict academic module DOCX documents from user-provided content organized by Prelim, Midterms, Prefinals, and Finals. Use when Codex needs to build or update a term-based module document, follow an exact .docx template layout, preserve user-supplied content without expansion, and enforce no-assessment, no-assumption, documentation-style output.
---

# Module Creator

## Overview

Create a final module `.docx` using only the user's provided content and the bundled template at `assets/Module Template Example.docx`.

Keep this skill low-freedom. Treat the template as the exact blueprint and the user's content as the only source of truth.

## Required Inputs

Require all of the following before creating the document:

- `subject`
- `focus`
- `prelim_content`
- `midterms_content`
- `prefinals_content`
- `finals_content`

Read [references/input-contract.md](references/input-contract.md) when the user input is incomplete, inconsistently labeled, or mixed into a longer request.

## Hard Rules

Follow these rules without exception:

1. Use only the content the user provides.
2. Do not add, infer, summarize, expand, or "improve" topics beyond the provided content.
3. Preserve the exact term order: `Prelim`, `Midterms`, `Prefinals`, `Finals`.
4. Follow the structure, layout, and formatting of `assets/Module Template Example.docx` exactly.
5. Keep the document clean, plain, and documentation-style. Do not add decorative formatting or creative layout changes.
6. Do not include examinations, quizzes, assessments, activities, worksheets, or evaluation sections unless the user explicitly provides content that must be reproduced as-is.
7. For non-IT or non-CS subjects, do not include code snippets or technical code blocks.
8. For IT or CS subjects, include only short code snippets and only when the user-provided content explicitly supports them. Never generate full files, full programs, or complete implementations.
9. Do not apply outside curriculum standards, style guides, or third-party formatting conventions.
10. Stay within module creation only. Do not perform adjacent tasks outside this scope.

## Missing Input Policy

Stop and ask for the missing required input when any required term content is absent or ambiguous.

Stop and ask when the bundled template file is missing or inaccessible. Do not create a substitute layout. Do not guess the template structure from memory or from a previous task.

Do not produce placeholders, partial sections, filler text, or speculative headings.

## Workflow

1. Check that all required inputs are present.
2. Check that `assets/Module Template Example.docx` is available.
3. Read the template and identify the exact structural pattern to replicate.
4. Map the user's content into the template without adding or removing conceptual material.
5. Keep term content in order: `Prelim -> Midterms -> Prefinals -> Finals`.
6. Apply code-snippet rules only if the subject is clearly IT/CS-related and the provided content explicitly includes or calls for short snippets.
7. Produce the final `.docx` document as the primary output.

## Output Rules

Produce a `.docx` document as the default output.

Use a professional, simple, documentation-style presentation.

If the user asks for explanation alongside the file, keep the explanation brief and focused on missing inputs, completion status, or constraints. Do not turn the response into a lesson, outline, or commentary unless requested.

## Guardrails for Content Handling

When the user provides rough notes, bullet fragments, or uneven detail across terms, preserve the substance exactly and organize it only as much as the template requires.

If a request tries to combine module creation with unrelated deliverables, complete only the module portion and ignore the rest unless the user explicitly changes scope.

If the user asks for extra sections that do not exist in the template, do not invent a new layout. Ask whether they want the template changed first.
