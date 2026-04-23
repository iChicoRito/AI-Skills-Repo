# Protocol Reference

## Execution control

- Wait for the exact trigger command `Go!` before generating code, screens, components, or database queries.
- Before `Go!`, only read instructions, inspect the project, confirm understanding, and ask clarifying questions.
- After `Go!`, execute all objectives exactly as specified.
- Follow React Native with Expo conventions.
- Prefer Expo Router and `app/` routes unless the project already uses another navigation structure.
- Use Gluestack UI as the primary component system.
- Use `react-hook-form` with `zodResolver`.
- Use `@supabase/supabase-js` with `expo-secure-store` for auth persistence.
- Use only `pnpm` for terminal commands.
- Add proper minimal comments for functions and sections.
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

## Package manager rules

- Use only `pnpm`.
- Allowed commands:
  - `pnpm install`
  - `pnpm add <package-name>`
  - `pnpm add -D <package-name>`
  - `pnpm <script-name>`
- Never use:
  - `npm`
  - `yarn`
  - `bun`

## Navigation and structure rules

- Default to Expo Router for new projects.
- Use:
  - `app/_layout.tsx` for root layout
  - `app/(group)/screen.tsx` or `app/feature/index.tsx` for routes
  - `components/` for reusable components
  - `components/ui/` for shared UI wrappers and Gluestack-based primitives
  - `lib/supabase/client.ts` for the app Supabase client
  - `lib/supabase/auth-storage.ts` for SecureStore-backed storage helpers
  - `lib/validations/` for Zod schemas
- If the project already uses React Navigation or another structure, follow the existing structure unless the user requests a migration.

## Expo rules

- Prefer Expo-managed workflow libraries.
- Avoid libraries that require native linking or prebuild unless the user explicitly accepts that requirement.
- Use `expo-image` or Expo-supported image solutions when image performance matters.
- Use `expo-router` for navigation in new builds.
- Use `EXPO_PUBLIC_` prefixed environment variables for client-safe values.
- Keep platform-specific code minimal and only introduce `.ios.tsx` or `.android.tsx` files when required.

## Gluestack UI rules

- Prefer Gluestack UI components before raw `View`, `Text`, `Pressable`, or custom wrappers when a matching component exists.
- Reuse the project's existing Gluestack theme tokens, variants, and size scales.
- Keep screen structure consistent:
  - top-level safe area or screen container
  - header area
  - content section
  - footer action area when needed
- Do not create one-off styling systems that bypass Gluestack patterns unless the project already does so.

## Icon rules

- Use `@expo/vector-icons` only unless the project already has a locked icon system.
- Keep icon usage consistent across the app.
- Prefer moderate icon sizes and align them with text baselines and touch targets.
- Never mix multiple icon libraries in the same feature without explicit approval.

## Form rules

- Use `react-hook-form`, `zod`, and `@hookform/resolvers`.
- Store schemas in `lib/validations/[feature].schema.ts`.
- Use `useForm` with `zodResolver`.
- Keep one shared form standard across create, edit, profile, settings, and filter flows.
- Keep label placement, helper text, validation timing, error text, and submit button placement consistent.
- Prefer validation on submit with field-level follow-up guidance.
- Keep forms single-column unless the device size clearly supports a more complex layout.

## Loading and feedback rules

- Always show a visible loading state for submit, save, refresh, delete, sign-in, and sign-out flows.
- Disable buttons while loading.
- Show explicit empty states instead of blank screens.
- Show clear retry affordances on fetch failures.
- Keep success, error, empty, and loading patterns consistent across screens.
- Prefer lightweight toast or inline status messaging patterns already used by the project.

## Mobile layout and accessibility rules

- Design for phones first.
- Keep touch targets comfortable.
- Respect safe areas.
- Avoid dense headers, crowded toolbars, and side-by-side content that reduces readability on narrow screens.
- Prefer full-screen routes or bottom sheets for long flows.
- Keep labels readable and avoid relying on color alone for status.
- Ensure important actions remain reachable above the keyboard when forms are open.
- Use keyboard-aware patterns where form length or screen size requires them.
- Maintain accessible names for buttons, icons, and inputs.

## Styling rules

- Use solid colors by default.
- Avoid gradients unless the user explicitly requests them.
- Reuse Gluestack tokens and variants before adding custom style values.
- Keep spacing and typography moderate.
- Avoid oversized display text unless the existing design system already uses it.
- Keep cards, list items, and actions visually consistent across features.

## Supabase setup

- Install:

```bash
pnpm add @supabase/supabase-js expo-secure-store
```

- Use a centralized client helper.
- Persist auth sessions with a SecureStore-backed adapter.
- Keep environment variables in Expo-safe format:
  - `EXPO_PUBLIC_SUPABASE_URL`
  - `EXPO_PUBLIC_SUPABASE_ANON_KEY`
- Use simple auth and fetch flows before introducing abstraction layers.

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

## Comment rules

- Use `//` comments only for TypeScript and JavaScript.
- Use short comments only.
- Never use JSDoc.
- Add a simple `//` comment above every function.
- Add a simple `//` comment above every component.
- Use section comments like:

```ts
// ==================== SECTION NAME ====================
```

## Coding standards

- Use strict TypeScript.
- Do not use `any`.
- Use function components with typed props.
- Use PascalCase for component files.
- Use kebab-case for folders.
- Use camelCase for variables.
- Use the `Schema` suffix for Zod schemas.
- Prefer simple hooks and utilities over layered abstractions.

## Simplification rules

- Prefer simple patterns over complex abstractions.
- Use:
  - `react-hook-form`
  - `zod`
  - `@hookform/resolvers`
  - `@supabase/supabase-js`
  - `expo-secure-store`
- Avoid:
  - `formik`
  - `yup`
  - `redux`
  - `zustand`
  - `react-query`

## Delivery rules

- For new files, provide full file content with the path.
- For small modifications, provide:
  - the file path
  - the old code block
  - the replacement block
  - a brief reason
- Always include:
  - TypeScript types
  - `//` comments for functions and sections
  - one icon system only
  - mobile-friendly layout decisions

## Working defaults

- If the project already contains matching conventions, follow them as long as they do not violate this protocol.
- If a request conflicts with this protocol, ask for clarification before implementation.
- If the user has not said `Go!`, stay in analysis mode.
