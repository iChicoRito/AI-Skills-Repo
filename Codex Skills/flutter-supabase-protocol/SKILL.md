---
name: flutter-supabase-protocol
description: Enforce a strict Flutter + Supabase development protocol with a gated "Go!" execution flow. Use when Codex must analyze or implement Flutter app work under this exact protocol, especially for Material 3 apps, go_router routing, Riverpod state management, Supabase auth or database flows, feature-first architecture, SQL artifact discipline, RLS-aware design, forms, and mobile-first UI consistency.
---

# Flutter Supabase Protocol

## Start in two phases

- Treat every request as phase one until the user says `Go!`.
- Before `Go!`, only:
  - read and analyze instructions
  - inspect the project structure
  - confirm understanding
  - ask clarifying questions when needed
- Before `Go!`, do not:
  - generate widgets or screens
  - create services or repositories
  - write database queries
- After `Go!`, execute every requested objective exactly as specified.
- After `Go!`, do not introduce alternative approaches unless the user asks.

## Follow the non-negotiables

- Use Flutter with Dart null safety only.
- Prefer Material 3 unless the project already follows another approved design system.
- Prefer `go_router` for routing in new work unless the project already uses another router.
- Prefer `flutter_riverpod` for shared app state unless the project already uses another stable state approach.
- Use Supabase through `supabase_flutter`.
- Use only `flutter pub add`, `flutter pub remove`, and `flutter pub get` for package management.
- Add minimal `//` comments only when they genuinely help scan complex logic.
- Never use comments as a substitute for clear naming.
- Never delete files without explicit permission.

## Protect files and scope

- Modify only the files required by the request.
- Create new files, update existing files, add code blocks, or edit specific sections when needed.
- If deletion is necessary, stop and ask for confirmation first using the user's preferred yes or no confirmation flow.
- Never batch-delete files or remove folders without explicit approval.

## Build with the required stack

- Use Flutter and Dart conventions already present in the project when they do not conflict with this protocol.
- Prefer `go_router` for navigation.
- Prefer `flutter_riverpod` for app state.
- Use `supabase_flutter` for auth, session, and database access.
- Prefer native Flutter forms unless the project already uses another consistent form package.
- Avoid overlapping packages that solve the same concern.

## Keep the implementation simple

- Prefer simple working code over layered abstractions.
- Use:
  - local widget state for small UI interactions
  - Riverpod providers for shared async or app-level state
  - `try/catch` for async, repository, and Supabase error handling
  - feature-first organization
- Avoid:
  - premature repository or use-case layers
  - unnecessary code generation
  - global mutable singletons
  - multiple state management libraries in one feature

## Respect project structure

- Use:
  - `lib/app/` for app bootstrap, router, theme, and guards
  - `lib/core/` for shared constants, services, and utilities
  - `lib/features/` for feature-based modules
  - `lib/shared/widgets/` for reusable UI
  - `lib/core/supabase/` for Supabase bootstrap helpers when shared broadly
- Within a feature, prefer:
  - `data/`
  - `domain/`
  - `presentation/`
- Keep structure proportional to project size and avoid forcing heavy layering into small apps.

## Implement forms and loading states consistently

- Keep labels, helper text, validation messages, and action placement consistent across screens.
- Prefer one-column forms on phones.
- Always show a visible loading state during submit, save, refresh, delete, sign-in, sign-out, or button-triggered async actions.
- Disable relevant actions while async work is running.
- Always show explicit loading, empty, error, and success states where data is involved.

## Enforce mobile UI constraints

- Build mobile-first for phones before expanding to tablets.
- Respect safe areas and keyboard behavior.
- Keep touch targets comfortable.
- Avoid cramped side-by-side layouts on small screens.
- Prefer full-screen flows or bottom sheets for longer interactions.
- Keep spacing, color, and typography consistent through the app theme.

## Use the exported color token catalog

- Use the exported SCSS color tokens listed in the protocol reference as the available app color catalog.
- Do not decide primary, secondary, accent, background, border, text, icon, component, status, focus, overlay, or state color mappings unless the user explicitly provides them.
- Do not create a 60-30-10 palette unless the user provides the mapping.
- Keep color token values centralized in the app theme or token layer when the user-defined mapping is available.

## Use the approved typography system

- Use the exported Figma font family tokens:
  - sans: `Inter`
  - serif: `Georgia`
  - mono: `Roboto Mono`
- Use `Inter` as the default app UI font family unless an existing project token layer maps the exported `sans` token differently.
- Use only the approved weights when needed:
  - thin
  - extralight
  - light
  - normal
  - medium
  - semibold or semi-bold
  - bold
  - extrabold
  - black
- Keep typography centralized in the app theme instead of mixing per-screen font or text color decisions.

## Handle Supabase and database work carefully

- Initialize Supabase once at app startup.
- Keep the client accessible through a centralized helper or provider.
- Store auth and session handling in a dedicated auth flow.
- Respect RLS-aware designs for every data access pattern.
- Save every database artifact under `database/` if the project stores SQL alongside the app.
- Always enable RLS on new tables.
- Always add matching policies in `database/policies/`.
- Keep schema reference files current in `database/schema/`.

## Deliver code in the required format

- For new files, provide the full file content with the path.
- For small edits, provide the changed section with a clear replacement format and a brief reason.
- Always include:
  - file path
  - typed Dart code
  - clear widget, provider, repository, or service responsibilities
  - mobile-friendly layout decisions

## Use the detailed protocol reference

- Read [references/protocol-reference.md](references/protocol-reference.md) before making edits.
- Use it for:
  - routing defaults
  - Riverpod guidance
  - Supabase bootstrap and auth rules
  - approved color palette and status colors
  - database folder and SQL rules
  - form and loading patterns
  - accessibility and responsiveness rules
  - testing expectations
  - package and delivery rules
