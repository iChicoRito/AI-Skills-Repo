---
name: sip-learning-outcomes
description: Create the Learning Outcomes section of a School Improvement Plan (SIP) as a strict DOCX document using an old SIP file as the exact template. Use when Codex needs to generate or update term-based SIP learning outcomes from user-provided lecture notes, slides, syllabus material, or other extracted course content while preserving the old SIP structure and avoiding added topics, examples, assessments, or external standards.
---

# SIP Learning Outcomes

## Overview

Create the Learning Outcomes section of an SIP `.docx` using only the user's provided source material and the bundled old SIP reference file at `assets/Old SIP Reference.docx`.

Keep this skill low-freedom. Treat the old SIP document as the exact blueprint and treat the user's extracted content as the only source of truth.

## Required Inputs

Require all of the following before creating the document:

- `subject`
- `focus`
- `prelim_content`
- `midterms_content`
- `prefinals_content`
- `finals_content`

Read [references/input-contract.md](references/input-contract.md) when the request is incomplete, loosely organized, or spread across multiple messages.

## Hard Rules

Follow these rules without exception:

1. Use only the content the user provides.
2. Do not add, infer, expand, or introduce new topics, examples, explanations, or standards.
3. Preserve the exact term order: `Prelim`, `Midterms`, `Prefinals`, `Finals`.
4. Follow the structure, layout, and formatting of `assets/Old SIP Reference.docx` exactly.
5. Keep the document clean, plain, and documentation-style. Do not add decorative formatting or creative layout changes.
6. Rewrite provided source material into concise measurable learning outcomes only when needed. Keep that rewrite within the exact topic boundaries supplied by the user.
7. Keep the SIP learning outcomes section text-only for all subjects, including IT and CS subjects. Do not include code snippets, technical code blocks, or full files.
8. Do not include examinations, quizzes, assessments, activities, worksheets, or evaluation sections unless the user explicitly provides content that must be reproduced as-is inside the learning outcomes section.
9. Do not apply outside curriculum standards, style guides, curriculum mappings, or third-party formatting conventions.
10. Stay within SIP learning outcomes creation only. Do not perform adjacent document tasks outside this scope.

## Missing Input Policy

Stop and ask for the missing required input when any term content is absent, unclear, or merged in a way that prevents reliable term assignment.

Stop and ask when the bundled SIP template file is missing or inaccessible. Do not invent a substitute SIP format. Do not guess the structure from memory or from prior tasks.

Do not produce placeholders, partial sections, filler text, or speculative outcomes.

## Workflow

1. Check that all required inputs are present.
2. Check that `assets/Old SIP Reference.docx` is available.
3. Read the SIP reference file and identify the exact Learning Outcomes structure and formatting to preserve.
4. Review the user's source material for each term.
5. Convert source material into concise measurable learning outcomes only when the source is not already written as outcomes.
6. Keep each outcome aligned with the supplied `focus` and with the topics present in the provided term content.
7. Preserve term order: `Prelim -> Midterms -> Prefinals -> Finals`.
8. Produce the final SIP `.docx` as the primary output.

## Output Rules

Produce a `.docx` document as the default output.

Preserve the old SIP structure exactly. Update content only.

If the user asks for explanation alongside the file, keep the explanation brief and focused on completion status, missing inputs, or constraints. Do not turn the response into extended teaching or commentary unless requested.

## Guardrails for Outcome Writing

When the source material is already written as learning outcomes, preserve the substance and wording as much as possible while fitting the old SIP layout.

When the source material is raw, fragmented, or extracted from slides or lecture notes, convert it into short formal learning outcomes without introducing new concepts.

If the request mixes SIP learning outcomes with unrelated outputs, complete only the SIP learning outcomes portion unless the user explicitly changes scope.

If the user requests new sections that are not part of the old SIP layout, stop and ask whether the template itself should be changed first.
