# Protocol Reference

## Execution control

- Wait for the exact trigger command `Go!` before generating widgets, screens, services, routes, or database code.
- Before `Go!`, only read instructions, inspect the project, confirm understanding, and ask clarifying questions.
- After `Go!`, execute all objectives exactly as specified.
- Follow Flutter and Dart null-safety conventions.
- Prefer Material 3 unless the project already follows another approved design system.
- Prefer `go_router` for navigation in new work.
- Prefer `flutter_riverpod` for shared app state in new work.
- Use `supabase_flutter` for Supabase integration.
- Use only Flutter package commands.
- Do not provide alternative approaches unless requested.

## File operations

- Never delete files without explicit permission.
- If deletion is required, ask first and wait for confirmation.
- Use this confirmation style:

```text
This action will delete [filename]. Are you sure? (yes/no)
```

- Safe operations:
  - create new files
  - update existing files
  - add code blocks
  - edit specific sections
- Strictly prohibit:
  - deleting files without asking
  - batch deletions
  - removing entire folders without confirmation

## Package rules

- Use only:
  - `flutter pub add <package>`
  - `flutter pub remove <package>`
  - `flutter pub get`
- Prefer stable, maintained packages with strong Flutter adoption.
- Avoid mixing libraries that solve the same concern.
- Do not edit `pubspec.yaml` manually unless necessary for a precise change.

## Project structure rules

- Prefer this structure for new or clean projects:
  - `lib/app/`
  - `lib/core/`
  - `lib/features/`
  - `lib/shared/widgets/`
  - `lib/core/supabase/`
- Inside each feature, prefer:
  - `data/`
  - `domain/`
  - `presentation/`
- Keep the structure proportional to the project's actual size and complexity.

## Navigation rules

- Prefer `go_router` in new projects.
- Keep route definitions centralized.
- Use route guards for auth, onboarding, or role-sensitive flows.
- Keep navigation predictable and declarative.
- If the project already uses another routing approach, follow it unless the user requests a migration.

## State management rules

- Prefer `flutter_riverpod`.
- Use local widget state for simple and short-lived UI interactions.
- Use providers for shared app state, async loading, settings, auth, and feature data.
- Avoid:
  - `provider`
  - `bloc`
  - `getx`
  - `mobx`
unless the project already depends on them.

## Supabase rules

- Use `supabase_flutter` only.
- Initialize Supabase once at startup.
- Keep the client accessible through a small, centralized abstraction.
- Keep auth, profile, and session logic in a dedicated auth area.
- Use typed models or DTOs when it improves clarity for repeated payloads.
- Keep database access patterns explicit and easy to trace.
- Respect RLS for every table and query path.

## Database workflow

- If the project stores SQL in the repo, keep all database files under `database/`.
- Use this structure when database artifacts are needed:
  - `database/functions/`
  - `database/policies/`
  - `database/schema/`
  - `database/sql/tables/`
  - `database/sql/indexes/`
  - `database/sql/views/`
  - `database/sql/triggers/`
  - `database/sql/realtime/`
  - `database/sql/migrations/`
- Every new table must enable RLS.
- Every new table must add matching policies in `database/policies/`.
- Keep schema reference files current in `database/schema/`.
- Save queries before execution when the project uses tracked SQL artifacts.

## Form rules

- Prefer native Flutter forms with:
  - `Form`
  - `TextFormField`
  - validators
- Only introduce form helper packages when the project already uses them or the request truly needs them.
- Keep validation messages, spacing, field order, helper text, and action placement consistent.
- Disable submit buttons while submitting.
- Show a visible progress indicator during form submission.

## UI and responsiveness rules

- Design for phones first.
- Use Material 3 theming as the primary design baseline.
- Keep colors, typography, spacing, and shape in the app theme rather than hardcoding values across widgets.
- Respect safe areas.
- Handle keyboard overlap for forms and bottom actions.
- Keep tablet layouts readable without forcing desktop-like density.
- Prefer extracted widgets once a build method becomes hard to scan.

## Figma token primitive rules

- Use the exported Figma token primitives as the source of truth for spacing, typography, radius, shadows, breakpoints, containers, opacity, blur, and border widths.
- When the JSON and SCSS exports differ, use the SCSS export because it includes the complete color scale, letter spacing tokens, and conventional opacity values.
- Centralize these values in the Flutter theme, theme extensions, or a dedicated token file before using them across screens.
- Do not hardcode token values repeatedly inside feature widgets.
- Preserve exported token names where practical so Flutter code stays traceable to Figma.

## Exported color tokens

- Use the exported SCSS color tokens as the source of truth for available app colors.
- Keep this list as a raw token catalog only; do not infer component, status, text, or theme mappings from it.
- Component color roles, semantic aliases, and palette decisions must be defined separately by the user.
- Prefer named token usage over raw hex values when implementing Flutter theme constants.

  - color slate-50: `#F8FAFC`
  - color slate-100: `#F1F5F9`
  - color slate-200: `#E2E8F0`
  - color slate-300: `#CBD5E1`
  - color slate-400: `#94A3B8`
  - color slate-500: `#64748B`
  - color slate-600: `#475569`
  - color slate-700: `#334155`
  - color slate-800: `#1E293B`
  - color slate-900: `#0F172A`
  - color slate-950: `#020617`
  - color gray-50: `#F9FAFB`
  - color gray-100: `#F3F4F6`
  - color gray-200: `#E5E7EB`
  - color gray-300: `#D1D5DB`
  - color gray-400: `#9CA3AF`
  - color gray-500: `#6B7280`
  - color gray-600: `#4B5563`
  - color gray-700: `#374151`
  - color gray-800: `#1F2937`
  - color gray-900: `#111827`
  - color gray-950: `#030712`
  - color zinc-50: `#FAFAFA`
  - color zinc-100: `#F4F4F5`
  - color zinc-200: `#E4E4E7`
  - color zinc-300: `#D4D4D8`
  - color zinc-400: `#A1A1AA`
  - color zinc-500: `#71717A`
  - color zinc-600: `#52525B`
  - color zinc-700: `#3F3F46`
  - color zinc-800: `#27272A`
  - color zinc-900: `#18181B`
  - color zinc-950: `#09090B`
  - color neutral-50: `#FAFAFA`
  - color neutral-100: `#F5F5F5`
  - color neutral-200: `#E5E5E5`
  - color neutral-300: `#D4D4D4`
  - color neutral-400: `#A3A3A3`
  - color neutral-500: `#737373`
  - color neutral-600: `#525252`
  - color neutral-700: `#404040`
  - color neutral-800: `#262626`
  - color neutral-900: `#171717`
  - color neutral-950: `#0A0A0A`
  - color stone-50: `#FAFAF9`
  - color stone-100: `#F5F5F4`
  - color stone-200: `#E7E5E4`
  - color stone-300: `#D6D3D1`
  - color stone-400: `#A8A29E`
  - color stone-500: `#78716C`
  - color stone-600: `#57534E`
  - color stone-700: `#44403C`
  - color stone-800: `#292524`
  - color stone-900: `#1C1917`
  - color stone-950: `#0C0A09`
  - color red-50: `#FEF2F2`
  - color red-100: `#FEE2E2`
  - color red-200: `#FECACA`
  - color red-300: `#FCA5A5`
  - color red-400: `#F87171`
  - color red-500: `#EF4444`
  - color red-600: `#DC2626`
  - color red-700: `#B91C1C`
  - color red-800: `#991B1B`
  - color red-900: `#7F1D1D`
  - color red-950: `#450A0A`
  - color orange-50: `#FFF7ED`
  - color orange-100: `#FFEDD5`
  - color orange-200: `#FED7AA`
  - color orange-300: `#FDBA74`
  - color orange-400: `#FB923C`
  - color orange-500: `#F97316`
  - color orange-600: `#EA580C`
  - color orange-700: `#C2410C`
  - color orange-800: `#9A3412`
  - color orange-900: `#7C2D12`
  - color orange-950: `#431407`
  - color amber-50: `#FFFBEB`
  - color amber-100: `#FEF3C7`
  - color amber-200: `#FDE68A`
  - color amber-300: `#FCD34D`
  - color amber-400: `#FBBF24`
  - color amber-500: `#F59E0B`
  - color amber-600: `#D97706`
  - color amber-700: `#B45309`
  - color amber-800: `#92400E`
  - color amber-900: `#78350F`
  - color amber-950: `#451A03`
  - color yellow-50: `#FEFCE8`
  - color yellow-100: `#FEF9C3`
  - color yellow-200: `#FEF08A`
  - color yellow-300: `#FDE047`
  - color yellow-400: `#FACC15`
  - color yellow-500: `#EAB308`
  - color yellow-600: `#CA8A04`
  - color yellow-700: `#A16207`
  - color yellow-800: `#854D0E`
  - color yellow-900: `#713F12`
  - color yellow-950: `#422006`
  - color lime-50: `#F7FEE7`
  - color lime-100: `#ECFCCB`
  - color lime-200: `#D9F99D`
  - color lime-300: `#BEF264`
  - color lime-400: `#A3E635`
  - color lime-500: `#84CC16`
  - color lime-600: `#65A30D`
  - color lime-700: `#4D7C0F`
  - color lime-800: `#3F6212`
  - color lime-900: `#365314`
  - color lime-950: `#1A2E05`
  - color green-50: `#F0FDF4`
  - color green-100: `#DCFCE7`
  - color green-200: `#BBF7D0`
  - color green-300: `#86EFAC`
  - color green-400: `#4ADE80`
  - color green-500: `#22C55E`
  - color green-600: `#16A34A`
  - color green-700: `#15803D`
  - color green-800: `#166534`
  - color green-900: `#14532D`
  - color green-950: `#052E16`
  - color emerald-50: `#ECFDF5`
  - color emerald-100: `#D1FAE5`
  - color emerald-200: `#A7F3D0`
  - color emerald-300: `#6EE7B7`
  - color emerald-400: `#34D399`
  - color emerald-500: `#10B981`
  - color emerald-600: `#059669`
  - color emerald-700: `#047857`
  - color emerald-800: `#065F46`
  - color emerald-900: `#064E3B`
  - color emerald-950: `#022C22`
  - color teal-50: `#F0FDFA`
  - color teal-100: `#CCFBF1`
  - color teal-200: `#99F6E4`
  - color teal-300: `#5EEAD4`
  - color teal-400: `#2DD4BF`
  - color teal-500: `#14B8A6`
  - color teal-600: `#0D9488`
  - color teal-700: `#0F766E`
  - color teal-800: `#115E59`
  - color teal-900: `#134E4A`
  - color teal-950: `#042F2E`
  - color cyan-50: `#ECFEFF`
  - color cyan-100: `#CFFAFE`
  - color cyan-200: `#A5F3FC`
  - color cyan-300: `#67E8F9`
  - color cyan-400: `#22D3EE`
  - color cyan-500: `#06B6D4`
  - color cyan-600: `#0891B2`
  - color cyan-700: `#0E7490`
  - color cyan-800: `#155E75`
  - color cyan-900: `#164E63`
  - color cyan-950: `#083344`
  - color sky-50: `#F0F9FF`
  - color sky-100: `#E0F2FE`
  - color sky-200: `#BAE6FD`
  - color sky-300: `#7DD3FC`
  - color sky-400: `#38BDF8`
  - color sky-500: `#0EA5E9`
  - color sky-600: `#0284C7`
  - color sky-700: `#0369A1`
  - color sky-800: `#075985`
  - color sky-900: `#0C4A6E`
  - color sky-950: `#082F49`
  - color blue-50: `#EFF6FF`
  - color blue-100: `#DBEAFE`
  - color blue-200: `#BFDBFE`
  - color blue-300: `#93C5FD`
  - color blue-400: `#60A5FA`
  - color blue-500: `#3B82F6`
  - color blue-600: `#2563EB`
  - color blue-700: `#1D4ED8`
  - color blue-800: `#1E40AF`
  - color blue-900: `#1E3A8A`
  - color blue-950: `#172554`
  - color indigo-50: `#EEF2FF`
  - color indigo-100: `#E0E7FF`
  - color indigo-200: `#C7D2FE`
  - color indigo-300: `#A5B4FC`
  - color indigo-400: `#818CF8`
  - color indigo-500: `#6366F1`
  - color indigo-600: `#4F46E5`
  - color indigo-700: `#4338CA`
  - color indigo-800: `#3730A3`
  - color indigo-900: `#312E81`
  - color indigo-950: `#1E1B4B`
  - color violet-50: `#F5F3FF`
  - color violet-100: `#EDE9FE`
  - color violet-200: `#DDD6FE`
  - color violet-300: `#C4B5FD`
  - color violet-400: `#A78BFA`
  - color violet-500: `#8B5CF6`
  - color violet-600: `#7C3AED`
  - color violet-700: `#6D28D9`
  - color violet-800: `#5B21B6`
  - color violet-900: `#4C1D95`
  - color violet-950: `#2E1065`
  - color purple-50: `#FAF5FF`
  - color purple-100: `#F3E8FF`
  - color purple-200: `#E9D5FF`
  - color purple-300: `#D8B4FE`
  - color purple-400: `#C084FC`
  - color purple-500: `#A855F7`
  - color purple-600: `#9333EA`
  - color purple-700: `#7E22CE`
  - color purple-800: `#6B21A8`
  - color purple-900: `#581C87`
  - color purple-950: `#3B0764`
  - color fuchsia-50: `#FDF4FF`
  - color fuchsia-100: `#FAE8FF`
  - color fuchsia-200: `#F5D0FE`
  - color fuchsia-300: `#F0ABFC`
  - color fuchsia-400: `#E879F9`
  - color fuchsia-500: `#D946EF`
  - color fuchsia-600: `#C026D3`
  - color fuchsia-700: `#A21CAF`
  - color fuchsia-800: `#86198F`
  - color fuchsia-900: `#701A75`
  - color fuchsia-950: `#4A044E`
  - color pink-50: `#FDF2F8`
  - color pink-100: `#FCE7F3`
  - color pink-200: `#FBCFE8`
  - color pink-300: `#F9A8D4`
  - color pink-400: `#F472B6`
  - color pink-500: `#EC4899`
  - color pink-600: `#DB2777`
  - color pink-700: `#BE185D`
  - color pink-800: `#9D174D`
  - color pink-900: `#831843`
  - color pink-950: `#500724`
  - color rose-50: `#FFF1F2`
  - color rose-100: `#FFE4E6`
  - color rose-200: `#FECDD3`
  - color rose-300: `#FDA4AF`
  - color rose-400: `#FB7185`
  - color rose-500: `#F43F5E`
  - color rose-600: `#E11D48`
  - color rose-700: `#BE123C`
  - color rose-800: `#9F1239`
  - color rose-900: `#881337`
  - color rose-950: `#4C0519`
  - color black: `#000000`
  - color white: `#FFFFFF`

## Exported spacing tokens

- Use these spacing tokens, in logical pixels:
  - spacing 0: `0`
  - spacing 0.5: `2`
  - spacing 1: `4`
  - spacing 1.5: `6`
  - spacing 2: `8`
  - spacing 2.5: `10`
  - spacing 3: `12`
  - spacing 3.5: `14`
  - spacing 4: `16`
  - spacing 5: `20`
  - spacing 6: `24`
  - spacing 7: `28`
  - spacing 8: `32`
  - spacing 9: `36`
  - spacing 10: `40`
  - spacing 11: `44`
  - spacing 12: `48`
  - spacing 14: `56`
  - spacing 16: `64`
  - spacing 20: `80`
  - spacing 24: `96`
  - spacing 28: `112`
  - spacing 32: `128`
  - spacing 36: `144`
  - spacing 40: `160`
  - spacing 44: `176`
  - spacing 48: `192`
  - spacing 52: `208`
  - spacing 56: `224`
  - spacing 60: `240`
  - spacing 64: `256`
  - spacing 72: `288`
  - spacing 80: `320`
  - spacing 96: `384`

## Exported size and layout tokens

- Use these font size tokens, in logical pixels:
  - xs: `12`
  - sm: `14`
  - base: `16`
  - lg: `18`
  - xl: `20`
  - 2xl: `24`
  - 3xl: `30`
  - 4xl: `36`
  - 5xl: `48`
  - 6xl: `60`
  - 7xl: `72`
  - 8xl: `96`
  - 9xl: `128`
- Use these line height tokens, in logical pixels:
  - 1: `16`
  - 2: `20`
  - 3: `24`
  - 4: `28`
  - 5: `32`
  - 6: `36`
  - 7: `40`
  - 8: `48`
  - 9: `48`
  - 10: `60`
  - 11: `72`
  - 12: `96`
  - 13: `128`
- Use these breakpoint tokens, in logical pixels:
  - sm: `640`
  - md: `768`
  - lg: `1024`
  - xl: `1280`
  - 2xl: `1536`
- Use these container width tokens, in logical pixels:
  - xs: `320`
  - sm: `384`
  - md: `448`
  - lg: `512`
  - xl: `576`
  - 2xl: `672`
  - 3xl: `768`
  - 4xl: `896`
  - 5xl: `1024`
  - 6xl: `1152`
  - 7xl: `1280`

## Exported shape and effect tokens

- Use these border radius tokens, in logical pixels:
  - none: `0`
  - sm: `2`
  - default: `4`
  - md: `6`
  - lg: `8`
  - xl: `12`
  - 2xl: `16`
  - 3xl: `24`
  - full: `999`
- Use these border width tokens, in logical pixels:
  - 0: `0`
  - default: `1`
  - 2: `2`
  - 4: `4`
  - 8: `8`
- Use these blur tokens, in logical pixels:
  - none: `0`
  - sm: `4`
  - default: `8`
  - md: `12`
  - lg: `16`
  - xl: `24`
  - 2xl: `40`
  - 3xl: `64`
- Use these shadow tokens:
  - none: `none`
  - 2xs: `0px 1px 0px 0px rgb(0 0 0 / 0.05)`
  - xs: `0px 1px 2px 0px rgb(0 0 0 / 0.05)`
  - sm: `0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1)`
  - default: `0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1)`
  - md: `0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1)`
  - lg: `0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1)`
  - xl: `0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1)`
  - 2xl: `0px 25px 50px -12px rgb(0 0 0 / 0.25)`
  - inner: `inset 0px 2px 4px 0px rgb(0 0 0 / 0.05)`
- Use the exported SCSS opacity tokens exactly as exported:
  - 0: `0`
  - 5: `0.05`
  - 10: `0.1`
  - 20: `0.2`
  - 25: `0.25`
  - 30: `0.3`
  - 40: `0.4`
  - 50: `0.5`
  - 60: `0.6`
  - 70: `0.7`
  - 75: `0.75`
  - 80: `0.8`
  - 90: `0.9`
  - 95: `0.95`
  - 100: `1`

## Exported letter spacing tokens

- Use these letter spacing tokens, in logical pixels:
  - tighter: `-0.800000011920929`
  - tight: `-0.4000000059604645`
  - normal: `0`
  - wide: `0.4000000059604645`
  - wider: `0.800000011920929`
  - widest: `1.600000023841858`

## Color rules

- Use only the exported color tokens listed above until the user defines semantic roles.
- Do not decide primary, secondary, accent, background, border, text, icon, component, status, focus, overlay, or state colors without explicit user instructions.
- Do not create a 60-30-10 palette unless the user provides the mapping.
- If a Flutter theme requires placeholder colors before the user defines them, stop and ask for the missing color role mapping.

## Typography rules

- Use these exported font family tokens:
  - sans: `Inter`
  - serif: `Georgia`
  - mono: `Roboto Mono`
- Use `Inter` as the default app UI font family unless an existing project token layer maps the exported `sans` token differently.
- Use these exported font weight tokens:
  - thin: `100`
  - extralight: `200`
  - light: `300`
  - normal: `400`
  - medium: `500`
  - semibold: `600`
  - bold: `700`
  - extrabold: `800`
  - black: `900`
- Centralize font family, text styles, and text colors in the Flutter theme rather than redefining them ad hoc inside widgets.

## Async and feedback rules

- Always handle loading, empty, error, and success states explicitly.
- Use `try/catch` around async operations.
- Keep retry, refresh, and failure messaging consistent.
- Do not leave blank containers where a user needs feedback.
- Use snackbars, banners, or inline messages consistently based on the project pattern.

## Architecture rules

- Prefer feature-first organization over layer-first app roots.
- Separate presentation from data access.
- Keep repositories and services small and explicit.
- Do not over-abstract simple flows.
- Add domain or use-case layers only when the app complexity clearly benefits from them.

## Model and serialization rules

- Use plain Dart models first.
- Add `json_serializable` when serialization becomes repetitive.
- Add `freezed` only when immutable models, unions, or copy patterns bring real value.
- Avoid code generation heavy patterns for small apps.

## Testing rules

- Add widget tests for important UI flows when the request includes testing or when the feature is risk-prone.
- Add unit tests for non-trivial business logic.
- Prioritize auth guards, validation, and important async states.
- Avoid low-value or brittle tests.

## Coding standards

- Use strict null-safe Dart.
- Follow `flutter_lints` or stronger approved linting.
- Use meaningful names.
- Keep methods reasonably short.
- Extract widgets when it improves readability.
- Comment sparingly and only when structure alone is not enough.

## Delivery rules

- For new files, provide full file content with the path.
- For small modifications, provide:
  - the file path
  - the old code block
  - the replacement block
  - a brief reason
- Always include typed Dart code and clear separation of responsibilities.

## Working defaults

- If the project already contains matching conventions, follow them as long as they do not violate this protocol.
- If a request conflicts with this protocol, ask for clarification before implementation.
- If the user has not said `Go!`, stay in analysis mode.
