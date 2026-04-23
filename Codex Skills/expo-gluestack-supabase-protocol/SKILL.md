---
name: expo-gluestack-supabase-protocol
description: Enforce a strict React Native + Expo + Gluestack UI + Supabase development protocol with a gated "Go!" execution flow. Use when Codex must analyze or implement Expo mobile app work under this exact protocol, especially for Expo Router screens, Gluestack UI components, Supabase auth or data flows, react-hook-form plus zod forms, SecureStore session persistence, and mobile-first UI consistency.
---

# Expo Gluestack Supabase Protocol

## Start in two phases

- Treat every request as phase one until the user says `Go!`.
- Before `Go!`, only:
  - read and analyze instructions
  - inspect the project structure
  - confirm understanding
  - ask clarifying questions when needed
- Before `Go!`, do not:
  - generate app code
  - create screens or components
  - write database queries
- After `Go!`, execute every requested objective exactly as specified.
- After `Go!`, do not introduce alternative approaches unless the user asks.

## Follow the non-negotiables

- Use React Native with Expo conventions.
- Prefer Expo Router with `app/` routes unless the project already uses a different navigation system.
- Use Gluestack UI as the primary component system.
- Use simple Supabase patterns with `@supabase/supabase-js`.
- Persist Supabase auth sessions with `expo-secure-store`.
- Use `react-hook-form` with `zodResolver` for forms.
- Use only `pnpm` for package management and scripts.
- Add minimal `//` comments above every function and component.
- Add `// ==================== SECTION NAME ====================` for important sections.
- Never use JSDoc comments.
- Never delete files without explicit permission.

## Protect files and scope

- Modify only the files required by the request.
- Create new files, update existing files, add code blocks, or edit specific sections when needed.
- If deletion is necessary, stop and ask for confirmation first using the user's preferred yes or no confirmation flow.
- Never batch-delete files or remove folders without explicit approval.

## Build with the required stack

- Use `pnpm install`, `pnpm add`, `pnpm add -D`, and `pnpm <script>`.
- Never use `npm`, `yarn`, or `bun`.
- Use Gluestack UI components and patterns already installed in the project.
- Use icons from `@expo/vector-icons` only unless the project already has a locked icon standard.
- Never introduce `lucide-react-native`, `react-native-vector-icons`, or mixed icon systems without a user request.

## Keep the implementation simple

- Prefer simple working code over clever abstractions.
- Use:
  - `react-hook-form` for forms
  - `useState` for local loading and UI state
  - `useEffect` for data fetching when needed
  - `try/catch` for async error handling
  - Context only when state truly needs app-wide sharing
- Avoid:
  - `formik`
  - `yup`
  - `redux`
  - `zustand`
  - `react-query`

## Respect project structure

- Use `app/` for Expo Router screens and layouts when the project follows Expo Router.
- Keep shared UI in `components/`.
- Keep Gluestack wrappers and shared design primitives in `components/ui/` when the project uses that pattern.
- Store Supabase helpers in:
  - `lib/supabase/client.ts`
  - `lib/supabase/auth-storage.ts`
- Store Zod schemas in `lib/validations/`.
- Store constants in `lib/constants/` when shared across features.
- Use `hooks/` for reusable hooks only when the logic is reused.

## Implement forms and loading states consistently

- Build forms with `react-hook-form`, `zod`, and Gluestack form-friendly inputs.
- Always wire form validation through `zodResolver`.
- Keep labels, helper text, validation messages, and submit actions consistent across screens.
- Prefer one-column forms on mobile.
- Always show a loading spinner on submit, save, delete, refresh, or button-triggered async actions.
- Disable actions while loading or submitting.

## Enforce mobile UI constraints

- Build mobile-first for phones before expanding to tablets.
- Use solid colors only.
- Never use gradients unless the user explicitly requests them.
- Keep spacing comfortable for touch interactions.
- Avoid cramped multi-column layouts.
- Prefer bottom sheets, action sheets, or full screens for longer flows instead of small modal patterns.
- Keep typography moderate and readable.
- Preserve keyboard access, readable contrast, visible focus states where supported, and accessible labels for inputs and actions.

## Handle Expo and Supabase carefully

- Use Expo-compatible libraries only unless the user explicitly accepts a native prebuild requirement.
- Prefer `EXPO_PUBLIC_` environment variables for client-safe Expo configuration.
- Use `expo-secure-store` for auth token persistence.
- Keep the Supabase client simple and centralized.
- Save every database artifact under `database/` if the project stores SQL alongside the app.
- Always enable RLS on new tables.
- Always add matching policies in `database/policies/`.

## Deliver code in the required format

- For new files, provide the full file content with the path.
- For small edits, provide the changed section with a clear replacement format and a brief reason.
- Always include:
  - file path
  - TypeScript types
  - minimal `//` comments
  - one icon system only
  - mobile-friendly layout decisions

## Use the detailed protocol reference

- Read [references/protocol-reference.md](references/protocol-reference.md) before making edits.
- Use it for:
  - Expo Router defaults
  - Gluestack UI usage rules
  - mobile layout and accessibility rules
  - form and loading patterns
  - Supabase auth persistence rules
  - environment variable rules
  - database folder rules
  - comment style requirements
  - delivery formatting rules
