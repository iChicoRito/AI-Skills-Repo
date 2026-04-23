# Protocol Reference

## Execution control

- Wait for the exact trigger command `Go!` before generating code, components, or database queries.
- Before `Go!`, only read instructions, confirm understanding, and ask clarifying questions.
- After `Go!`, execute all objectives exactly as specified.
- Follow Next.js `14+` App Router conventions.
- Use shadcn/ui components from `components/ui/`.
- Implement Supabase with simple patterns.
- Use `react-hook-form` with `zodResolver` for forms.
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

## Icon rules

- Use Tabler Icons only.
- Install with:

```bash
pnpm add @tabler/icons-react
```

- Import with:

```tsx
import { IconName, Loader2 } from '@tabler/icons-react'
```

- Prefer `size={18}` or `size={20}`.
- Add Tailwind classes through `className`.
- Use `Loader2` with `animate-spin` for loading states.
- Never use:
  - `lucide-react`
  - `react-icons`
  - `@heroicons/react`

## UI design rules

### Responsiveness

- Always design mobile-first, then scale up for tablet, laptop, and desktop.
- Use these breakpoint defaults unless the existing project already defines an approved equivalent:
  - mobile: default and `<640px`
  - tablet: `sm` and `md`
  - laptop: `lg`
  - desktop: `xl` and above
- Every screen, form, table, card grid, dialog, drawer, and toolbar must remain usable on small screens.
- Avoid fixed widths that cause overflow or horizontal scrolling unless the pattern explicitly requires it.
- Stack related actions and fields on small screens, then expand to multi-column layouts only when space allows.
- Keep touch targets and spacing comfortable on phones.
- Check headers, filters, pagination, and sticky actions so they do not clip or overlap on narrow viewports.
- Do not introduce multi-column page sections, split panels, or dense action bars until the viewport clearly supports them.

### Table behavior

- Every table must have a defined small-screen behavior before implementation.
- Use one of these patterns:
  - priority columns with less important columns hidden on mobile
  - stacked card rows for mobile-first data browsing
  - controlled horizontal scroll when preserving tabular comparison is necessary
- Keep row actions accessible on small screens without causing overflow.
- Move dense row actions into menus when inline buttons become cramped.
- Keep filters, search, and pagination responsive and easy to reach on phones.

### Accessibility

- All interactive controls must be keyboard accessible.
- Preserve visible focus states for buttons, links, inputs, selects, tabs, dialogs, and menu triggers.
- Every input must have a clear label or accessible name.
- Pair helper text and validation text with the related field.
- Keep color contrast readable and do not rely on color alone to communicate status or errors.
- Ensure dialog, drawer, sheet, and popover content supports focus management and escape or close behavior.

### Colors

- Use solid colors only.
- Never use gradients.
- Prohibit:
  - `bg-gradient-to-*`
  - `from-*`
  - `via-*`
  - `to-*`
- Prefer:
  - `bg-background`
  - `bg-card`
  - `bg-popover`
  - `text-foreground`
  - `text-muted-foreground`
  - `red-500`
  - `green-500`
  - `yellow-500`
  - `blue-500`

### Sizing

- Do not use oversized UI values.
- Maximum text size is `text-lg`.
- Allowed text classes:
  - `text-xs`
  - `text-sm`
  - `text-base`
  - `text-lg`
- Allowed padding classes:
  - `p-1`
  - `p-2`
  - `p-3`
  - `p-4`
  - `px-1`
  - `px-2`
  - `px-3`
  - `px-4`
  - `py-1`
  - `py-2`
  - `py-3`
  - `py-4`
- Allowed margin classes:
  - `m-1`
  - `m-2`
  - `m-3`
  - `m-4`
  - `mx-1`
  - `mx-2`
  - `mx-3`
  - `mx-4`
  - `my-1`
  - `my-2`
  - `my-3`
  - `my-4`
- Allowed gap classes:
  - `gap-1`
  - `gap-2`
  - `gap-3`
  - `gap-4`
- Allowed width classes:
  - `w-auto`
  - `w-full`
  - `max-w-md`
  - `max-w-lg`
- Allowed height classes:
  - `h-auto`
  - `h-8`
  - `h-10`
  - `h-12`
- Allowed rounded classes:
  - `rounded`
  - `rounded-md`
  - `rounded-lg`
- Do not use:
  - `text-xl`, `text-2xl`, `text-3xl`
  - `p-5`, `p-6`, `p-8`, `p-10`
  - `m-5`, `m-6`, `m-8`, `m-10`
  - `gap-5`, `gap-6`, `gap-8`
  - `max-w-xl`, `max-w-2xl`, `max-w-3xl`
  - `h-14`, `h-16`, `h-20`
  - `rounded-xl`, `rounded-2xl`
  - `rounded-full` for containers

### Badge styles

- Use these exact classes:

```tsx
// Success badge
className="rounded-md border-0 bg-green-500/10 px-2.5 py-0.5 text-green-500"

// Error badge
className="rounded-md border-0 bg-rose-500/10 px-2.5 py-0.5 text-rose-500"

// Warning badge
className="rounded-md border-0 bg-yellow-500/10 px-2.5 py-0.5 text-yellow-500"

// Info badge
className="rounded-md border-0 bg-blue-500/10 px-2.5 py-0.5 text-blue-500"
```

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

- Use JSX comments like:

```tsx
{/* brief */}
```

- Use SQL comments like:

```sql
-- brief
```

## Project structure

- Routes: `app/folder-name/page.tsx`
- Layout: `app/layout.tsx`
- Middleware: `app/middleware.ts`
- UI components: `components/ui/`
- Supabase:
  - `lib/supabase/client.ts`
  - `lib/supabase/server.ts`
  - `lib/supabase/middleware.ts`
- Zod schemas: `lib/validations/`

## Database workflow

- Use the Supabase SQL Editor for all database changes.
- Do not use terminal migrations.
- Store all database files under `database/`.
- Use this structure:
  - `database/functions/`
  - `database/policies/`
  - `database/schema/`
  - `database/sql/tables/`
  - `database/sql/indexes/`
  - `database/sql/views/`
  - `database/sql/triggers/`
  - `database/sql/realtime/`
  - `database/sql/migrations/`
- Use descriptive file names such as:
  - `create_products_table.sql`
  - `add_category_column.sql`
  - `enable_realtime_products.sql`

### SQL file header format

```sql
-- ==================== [ACTION DESCRIPTION] ====================
-- File: database/[category]/[subcategory]/[filename].sql
-- Created: [date]
-- Purpose: [brief description]
```

### Required database rules

- Every SQL file must start with a title comment.
- Every new table must enable RLS.
- Every new table must add matching policies in `database/policies/`.
- Every new table must enable real-time in a separate file under `database/sql/realtime/`.
- Maintain schema reference files in `database/schema/`.
- Use `--` comments for complex SQL logic.
- Test queries before running in production.

### Real-time pattern

```sql
-- ==================== ENABLE REAL-TIME ON PRODUCTS ====================
-- File: database/sql/realtime/enable_realtime_products.sql
ALTER PUBLICATION supabase_realtime ADD TABLE products;
```

### Real-time status check

```sql
SELECT * FROM pg_publication_tables WHERE pubname = 'supabase_realtime';
```

### Strictly prohibit

- Creating database files outside `database/`
- Creating SQL files outside the required subfolders
- Running queries without saving to the proper folder first
- Running queries without title comments
- Creating tables without enabling RLS
- Creating tables without enabling real-time
- Creating tables without storing policies in `database/policies/`
- Skipping schema maintenance

## shadcn/ui rules

- Add components with:

```bash
pnpm dlx shadcn-ui@latest add <component-name>
```

- Use the generated components from `components/ui/`.

## Middleware rules

- Place middleware in `app/middleware.ts` when requested by the project.
- Use it for route protection and authentication.
- Redirect unauthenticated users to login.
- Add `//` comments that explain the middleware logic.

## Form rules

- Use `react-hook-form`, `zod`, and `@hookform/resolvers`.
- Install with:

```bash
pnpm add react-hook-form zod @hookform/resolvers
```

- Store schemas in `lib/validations/[feature].schema.ts`.
- Use `useForm` with `zodResolver`.
- Use shadcn form components:
  - `Form`
  - `FormField`
  - `FormItem`
  - `FormLabel`
  - `FormControl`
  - `FormMessage`
- Keep one shared form standard across create, edit, settings, and filter flows.
- Keep field spacing, label placement, helper text, validation messages, and submit areas consistent.
- Keep required-field indicators, placeholder behavior, helper-text tone, and error-message wording consistent.
- Prefer validation on submit plus field-level follow-up guidance unless the current project already uses a clear standard.
- Prefer one-column forms on mobile and introduce multi-column layouts only when the content still reads clearly.
- Keep primary and secondary form actions aligned consistently and responsive on small screens.
- Keep primary action placement consistent across forms.
- Use the same pattern for reset, cancel, destructive confirmation, and unsaved-change handling when those flows are present.

### Button loading pattern

```tsx
<Button type="submit" disabled={form.formState.isSubmitting}>
  {form.formState.isSubmitting ? (
    <>
      <Loader2 className="mr-2 h-4 w-4 animate-spin" />
      Loading...
    </>
  ) : (
    'Submit'
  )}
</Button>
```

### Loading requirements

- Always show a spinner during form submission.
- Always show a spinner during delete or update actions.
- Always show a spinner during button-triggered fetch actions.
- Use `Loader2` from `@tabler/icons-react`.
- Use loading text such as:
  - `Saving...`
  - `Deleting...`
  - `Loading...`

## Supabase setup

- Install:

```bash
pnpm add @supabase/ssr @supabase/supabase-js
```

- Use:
  - `lib/supabase/client.ts` for browser components
  - `lib/supabase/server.ts` for server components
  - `lib/supabase/middleware.ts` for route protection
- Required environment variables:
  - `NEXT_PUBLIC_SUPABASE_URL`
  - `NEXT_PUBLIC_SUPABASE_ANON_KEY`

## State management

- Use `react-hook-form` for forms.
- Use `useState` for:
  - loading
  - dialog state
  - drawer state
  - local data state

## Overlay component rules

- Standardize modal-like surfaces across the app, including `Dialog`, `Drawer`, `Sheet`, `Popover`, and confirmation prompts.
- Use `Dialog` for short focused tasks or confirmations on desktop-first flows.
- Use `Drawer` or `Sheet` when the interaction should feel natural on mobile or when vertical space is tighter.
- Use full-page routes instead of overlays for long forms, dense editing, or workflows with multiple sections.
- Keep overlay headers, descriptions, body spacing, footer actions, and dismiss controls consistent.
- Ensure overlays have responsive widths and heights, avoid clipped content, and support scrolling inside the content area when needed.
- Keep close button, cancel action, escape behavior, and outside-click behavior aligned with the use case and consistent across the app.
- Use stronger confirmation patterns for destructive actions instead of generic prompts.
- Do not create one-off modal, dialog, or drawer patterns when an existing shared structure can be reused.

## Performance rules

- Use the Next.js `Image` component for images.
- Add `'use client'` only when hooks are required.
- Use shadcn skeleton components for loading UI.

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
  - Tabler icons only
  - solid colors only

## Coding standards

- Use strict TypeScript.
- Do not use `any`.
- Use function components with typed props.
- Use:
  - PascalCase for component files
  - kebab-case for folders
  - `useCamelCase` for hooks
  - camelCase for variables
  - camelCase plus `Schema` suffix for schemas

## Error handling

- Show validation errors with `FormMessage`.
- Use shadcn sonner toast feedback for operations.
- For fetched data:
  - show skeleton while loading
  - show a retry message on error
  - show `No data found` when empty
- Keep loading, empty, success, and error states visually consistent across pages, cards, forms, and tables.
- Do not leave blank containers without an explicit loading, empty, or error state.

## Simplification rules

- Prefer simple patterns over complex abstractions.
- Keep these libraries:
  - `react-hook-form`
  - `zod`
  - `@hookform/resolvers`
  - `@tabler/icons-react`
- Avoid these libraries:
  - `lucide-react`
  - `react-icons`
  - `formik`
  - `yup`
  - `redux`
  - `zustand`
  - `react-query`

## Working defaults

- If the project already contains matching conventions, follow them as long as they do not violate this protocol.
- If a request conflicts with this protocol, ask for clarification before implementation.
- If the user has not said `Go!`, stay in analysis mode.
