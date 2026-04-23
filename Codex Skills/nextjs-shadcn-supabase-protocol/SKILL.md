---
name: nextjs-shadcn-supabase-protocol
description: Enforce a strict Next.js 14+ App Router, shadcn/ui, and Supabase development protocol with a gated "Go!" execution flow. Use when Codex must follow project-specific build rules for Next.js, shadcn/ui, Supabase, pnpm-only package management, React Hook Form with Zod, Tabler icons, SQL-file organization, no-gradient UI constraints, controlled file edits, and structured code delivery.
---

# Next.js shadcn Supabase Protocol

## Start in two phases

- Treat every request as phase one until the user says `Go!`.
- Before `Go!`, only:
  - read and analyze instructions
  - confirm understanding
  - ask clarifying questions when needed
- Before `Go!`, do not:
  - generate code
  - create components
  - write database queries
- After `Go!`, execute every requested objective exactly as specified.
- After `Go!`, do not introduce alternative approaches unless the user asks.

## Follow the non-negotiables

- Use Next.js `14+` App Router conventions.
- Use shadcn/ui components from `components/ui/`.
- Use simple Supabase patterns with `@supabase/ssr`.
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
- Add shadcn/ui components with `pnpm dlx shadcn-ui@latest add <component-name>`.
- Use Tabler icons from `@tabler/icons-react`.
- Never use `lucide-react`, `react-icons`, or `@heroicons/react`.

## Keep the implementation simple

- Prefer simple working code over clever abstractions.
- Use:
  - `react-hook-form` for forms
  - `useState` for loading, dialog, drawer, and local data state
  - `useEffect` for data fetching when needed
  - `try/catch` for async error handling
- Avoid:
  - `formik`
  - `yup`
  - `redux`
  - `zustand`
  - `react-query`

## Respect project structure

- Use `app/folder-name/page.tsx` for routes.
- Keep the main layout in `app/layout.tsx`.
- Put route protection middleware in `app/middleware.ts` when the project expects it there.
- Store Supabase helpers in:
  - `lib/supabase/client.ts`
  - `lib/supabase/server.ts`
  - `lib/supabase/middleware.ts`
- Store Zod schemas in `lib/validations/`.
- Use `components/ui/` for shadcn/ui components.

## Implement forms and loading states consistently

- Build forms with shadcn `Form`, `FormField`, `FormItem`, `FormLabel`, `FormControl`, and `FormMessage`.
- Always wire form validation through `zodResolver`.
- Keep forms unified across the app with the same field structure, spacing rhythm, label placement, help text style, validation message placement, and submit action layout.
- Prefer a shared form pattern for create, edit, filter, and settings flows instead of inventing per-page variations.
- Keep required markers, placeholder usage, helper text tone, validation timing, and primary or secondary action order consistent.
- Prefer one-column forms on mobile and only expand to multi-column layouts when readability stays strong.
- Use the same loading, empty, success, and error feedback pattern across all forms and data actions.
- Always show a loading spinner on submit, delete, refresh, or button-triggered async actions.
- Use `Loader2` from `@tabler/icons-react` with `animate-spin`.
- Disable buttons while loading.

## Enforce UI constraints

- Use solid colors only.
- Never use gradients.
- Keep typography, spacing, and widths in the allowed range from the reference file.
- Keep containers modest in size.
- Always consider responsiveness for mobile, tablet, laptop, and desktop layouts.
- Build mobile-first and verify layouts, forms, tables, dialogs, drawers, and action bars remain usable on small screens.
- Follow standard responsive breakpoints and only increase layout complexity when the viewport has enough space.
- Make tables responsive with a deliberate mobile strategy such as priority columns, stacked card presentation, or controlled horizontal scroll.
- Avoid overflow, clipped content, off-screen actions, and fixed widths that break responsive behavior.
- Keep modals, dialogs, drawers, sheets, popovers, and similar overlay surfaces visually and behaviorally consistent across the app.
- Use dialogs for short focused actions, drawers for constrained mobile-friendly flows, and keep sizing, padding, header, footer, and close actions standardized.
- Use full pages instead of overlays when the task is long, dense, or requires sustained editing.
- Always preserve keyboard access, visible focus states, readable contrast, and screen-reader friendly labels for forms and interactive UI.
- Use the exact colored badge classes from the reference file when success, error, warning, or info badges are needed.

## Handle Supabase and database work carefully

- Use SQL queries in the Supabase SQL Editor for every database change.
- Save every database artifact under `database/`.
- Always enable RLS on new tables.
- Always add matching policies in `database/policies/`.
- Always enable Supabase real-time for every new table using a separate SQL file.
- Keep schema reference files in `database/schema/`.

## Deliver code in the required format

- For new files, provide the full file content with the path.
- For small edits, provide the changed section with a clear replacement format and a brief reason.
- Always include:
  - file path
  - TypeScript types
  - minimal `//` comments
  - Tabler icons only
  - solid-color styling only

## Use the detailed protocol reference

- Read [references/protocol-reference.md](references/protocol-reference.md) before making edits.
- Use it for:
  - exact UI sizing limits
  - responsive layout rules
  - responsive breakpoint and table rules
  - dialog and drawer standards
  - accessibility rules
  - badge class strings
  - comment style requirements
  - database folder rules
  - SQL file metadata format
  - middleware expectations
  - form patterns
  - shared loading, empty, and error state patterns
  - delivery formatting rules
