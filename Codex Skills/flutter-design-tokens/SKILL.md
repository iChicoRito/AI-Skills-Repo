---
name: flutter-design-tokens
description: Apply the user's Flutter UI design token mapping for colors and typography. Use when Codex is implementing or reviewing Flutter UI that should follow the user's defined color scheme for backgrounds, cards, dialogs, badges, icons, chips, buttons, forms, text, and typography based on the exported Figma/Tailwind-style tokens.
---

# Flutter Design Tokens

Use this skill when Flutter UI must follow the user's defined visual system. These mappings are explicit decisions from the user and may be applied to components, screens, themes, and reusable widgets.

## Source Rules

- Use the token names first and keep raw hex values as verification comments or constants only when useful.
- Do not substitute nearby colors unless the requested token is unavailable in the project token layer.
- Keep values centralized in theme constants, theme extensions, or design token classes.
- Use `Inter` from `$font-family-sans` for the typography roles below.
- Preserve existing project architecture and component naming while applying these visual decisions.

## Color Scheme

### Base / Background

- Background fill: `$color-neutral-50` / `#FAFAFA`

### Cards / Dialog

- Border: `$color-neutral-100` / `#F5F5F5`
- Fill: `$color-white` / `#FFFFFF`

### Badge / Icons / Chips

Primary:

- Text: `$color-blue-500` / `#3B82F6`
- Fill: `$color-blue-100` / `#DBEAFE`
- Icon: `$color-blue-500` / `#3B82F6`

Secondary:

- Text: `$color-neutral-50` / `#404040`
- Fill: `$color-neutral-700` / `#E5E5E5`
- Icon: `$color-neutral-50` / `#404040`

Danger:

- Text: `$color-rose-500` / `#F43F5E`
- Fill: `$color-rose-100` / `#FFE4E6`
- Icon: `$color-rose-500` / `#F43F5E`

Success:

- Text: `$color-teal-500` / `#14B8A6`
- Fill: `$color-teal-100` / `#CCFBF1`
- Icon: `$color-teal-500` / `#14B8A6`

Warning:

- Text: `$color-amber-500` / `#F59E0B`
- Fill: `$color-amber-100` / `#FEF3C7`
- Icon: `$color-amber-500` / `#F59E0B`

### Buttons

Primary:

- Text: `$color-blue-50` / `#EFF6FF`
- Fill: `$color-blue-500` / `#3B82F6`
- Icon: `$color-blue-50` / `#EFF6FF`

Secondary:

- Text: `$color-neutral-50` / `#404040`
- Fill: `$color-neutral-700` / `#E5E5E5`
- Icon: `$color-neutral-50` / `#404040`

Danger:

- Text: `$color-rose-50` / `#FFF1F2`
- Fill: `$color-rose-500` / `#F43F5E`
- Icon: `$color-rose-50` / `#FFF1F2`

Success:

- Text: `$color-teal-50` / `#F0FDFA`
- Fill: `$color-teal-500` / `#14B8A6`
- Icon: `$color-teal-50` / `#F0FDFA`

Warning:

- Text: `$color-amber-50` / `#FFFBEB`
- Fill: `$color-amber-500` / `#F59E0B`
- Icon: `$color-amber-50` / `#FFFBEB`

### Forms

Input field:

- Border: `$color-neutral-200` / `#E5E5E5`
- Placeholder: `$color-neutral-400` / `#A3A3A3`

Dropdown:

- Border: `$color-neutral-200` / `#E5E5E5`
- Placeholder: `$color-neutral-400` / `#A3A3A3`

Checkbox:

- Border: `$color-blue-200` / `#BFDBFE`
- Fill: `$color-blue-500` / `#3B82F6`
- Icon: `$color-blue-50` / `#EFF6FF`

Checkbox card:

- Border: `$color-neutral-200` / `#E5E5E5`
- Fill: `$color-neutral-50` / `#FAFAFA`

### Text

- Title/Header: `$color-neutral-700` / `#404040`
- Sub-header: `$color-neutral-400` / `#A3A3A3`

## Typography

### Dialog / Modal Text Contents

Title/Header:

- Font family: `$font-family-sans` / `Inter`
- Font weight: `$font-weight-semibold` / `600`
- Font size: `$font-size-lg` / `18`

Sub-header / Paragraph:

- Font family: `$font-family-sans` / `Inter`
- Font weight: `$font-weight-normal` / `400`
- Font size: `$font-size-base` / `16`

### Cards Text Contents

Title/Header:

- Font family: `$font-family-sans` / `Inter`
- Font size: `$font-size-lg` / `18`
- Font weight: `$font-weight-semibold` / `600`

Sub-header / Paragraph:

- Font family: `$font-family-sans` / `Inter`
- Font size: `$font-size-base` / `16`
- Font weight: `$font-weight-normal` / `400`

### Pages / Nav Headers

Title/Header:

- Font family: `$font-family-sans` / `Inter`
- Font size: `$font-size-lg` / `18`
- Font weight: `$font-weight-semibold` / `600`

Sub-header:

- Font family: `$font-family-sans` / `Inter`
- Font size: `$font-size-base` / `16`
- Font weight: `$font-weight-normal` / `400`

## Padding and Radius

### Button

Padding / Radius:

- Left/Right: `$spacing-5` / `20`
- Top/Bottom: `$spacing-5` / `20`
- Radius: `$radius-xl` / `12`

### Cards / Dialog

Padding / Radius:

- Left/Right: `$spacing-8` / `32`
- Top/Bottom: `$spacing-6` / `24`
- Radius: `$radius-3xl` / `24`

## Implementation Guidance

- For Flutter, prefer defining these as `Color` constants, `TextStyle` constants, and theme extension fields.
- Map badge, chip, icon, and button variants directly to the named roles above.
- Use card/dialog fill and border values for modal surfaces, card containers, selection cards, and dialog panels unless a screen has more specific user instructions.
- Use the form mappings for `TextField`, `TextFormField`, dropdowns, checkboxes, and checkbox-card variants.
- If this skill is used together with `$flutter-protocol` or `$flutter-supabase-protocol`, this skill supplies the component color and typography mappings that those protocols intentionally leave undefined.
