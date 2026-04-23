# Laravel 11 Protocol Reference

Use this file as the detailed rules reference for the `laravel-11-ai-protocol` skill.

## Table of contents

- [Execution gate](#execution-gate)
- [Database rules](#database-rules)
- [Models](#models)
- [Controllers](#controllers)
- [Views](#views)
- [Routes](#routes)
- [Migrations and file creation](#migrations-and-file-creation)
- [Code delivery rules](#code-delivery-rules)
- [General coding style](#general-coding-style)

## Execution gate

- Treat `Go!` as the execution trigger.
- Treat only the exact token `Go!` as implementation approval unless the user explicitly says another phrase is equivalent.
- Before `Go!`, allow only:
  - reading and analyzing provided content
  - confirming understanding
  - asking clarifying questions when needed
- Before `Go!`, do not:
  - generate code
  - modify existing code
  - perform implementation tasks
- After `Go!`, do all of the following:
  - execute objectives exactly as specified
  - follow the user's project conventions strictly
  - follow Laravel framework behavior unless the user explicitly overrides it
  - follow naming conventions strictly
  - avoid deviating from the instructions

## Database rules

### Schema reference folder

- When direct database access is not available, use the `database/schema` folder as the source of truth for schema inspection and reference.
- Treat the files in `database/schema` as reference-only representations of the current database structure.
- Use the schema reference files to understand existing tables, columns, indexes, relationships, and constraints before planning database-related changes.
- Do not treat `database/schema` files as a replacement for real Laravel migrations.
- Whenever a real migration adds, edits, drops, renames, or removes database structures, update the corresponding file in `database/schema` so the reference stays synchronized with the actual schema.

### New databases or tables

- Create new tables with Laravel migrations only.
- Use `php artisan make:migration create_{table_name}_table`.
- Never manually create migration files.
- Always generate migration files through Artisan.

Reasons:

- portability across environments
- version-controlled schema changes
- rollback support

### Updating existing tables

- Prefer Laravel migrations for structural table changes, including:
- Require Laravel migrations for all structural table changes, regardless of scope, size, or urgency, including:
  - adding columns
  - dropping columns
  - altering field types or attributes
  - renaming columns or indexes
- Continue using Artisan-generated migration files instead of manually creating them.
- Do not use direct SQL for schema changes.
- If Laravel's schema builder alone is insufficient, still deliver the change through a migration file using the appropriate database statements inside the migration.

## Models

### Naming

- Name files as `{Name}Model.php`.
- Use singular StudlyCase names.
- End every model name with `Model`.
- Match the class name to the filename exactly.

Examples:

- `UserModel.php`
- `ProductModel.php`
- `OrderModel.php`

### Database representation

- Reflect the corresponding table structure accurately.
- Represent all relevant columns in the model configuration.
- Include required Eloquent relationships.
- Define either `$fillable` or `$guarded`; never leave both empty or undefined.

### Code style

- Use `camelCase` for method names.
- Add descriptive docblocks for properties and methods.
- Keep models focused on data interaction only.
- Do not put validation logic in models.
- Do not put unrelated business logic in models.

## Controllers

### Design

- Keep controllers clean, simple, and readable.
- Avoid deeply nested logic.
- Delegate heavier logic to services or models when needed.
- Use RESTful methods where applicable:
  - `index`
  - `create`
  - `store`
  - `show`
  - `edit`
  - `update`
  - `destroy`

### Input validation

- Use either:
  - Laravel `FormRequest` classes
  - inline `$request->validate()`
- Prefer `FormRequest` classes for non-trivial create/update flows.
- Apply specific validation rules per field.
- Avoid vague validation messages.
- Provide clear, user-friendly custom messages.
- Use SweetAlert2 to show validation errors and alerts to the user.
- Authorize sensitive actions such as create, update, delete, admin access, and protected resource access.
- Wrap multi-step write operations in `DB::transaction()` when partial completion would leave inconsistent data.

### AJAX integration

- Use jQuery + AJAX for Blade-based CRUD form submissions unless the existing project already uses another frontend pattern or the user requests normal form posting.
- Return JSON responses for AJAX submit handlers.
- Use proper HTTP status codes together with the JSON body when possible.
- Use this response structure:

Success response:

```json
{
  "status": "success",
  "message": "Descriptive success message"
}
```

Error response:

```json
{
  "status": "error",
  "message": "Descriptive error message",
  "errors": {}
}
```

Validation error example:

```json
{
  "status": "error",
  "message": "Please correct the highlighted fields.",
  "errors": {
    "name": [
      "The name field is required."
    ]
  }
}
```

## Views

### UI consistency

- Keep layouts modern, clean, and consistent.
- Preserve the established design system or layout template.

### AJAX form handling

- Use jQuery + AJAX for Blade-based CRUD forms unless the project already follows another frontend convention.
- Provide real-time validation feedback.
- Prevent default form submission.
- Display success and error states with SweetAlert2.
- Include CSRF protection for AJAX requests.
- Show loading states while a request is in progress.

Success SweetAlert2:

- `icon: success`
- `showConfirmButton: false`
- `timer: 2000`
- `timerProgressBar: true`

Confirmation SweetAlert2:

- `icon: warning`
- `showConfirmButton: true`
- `confirmButtonColor: #3475db`
- `showCancelButton: true`

Error SweetAlert2:

- `icon: error`
- `showConfirmButton: true`
- `confirmButtonColor: #3475db`

### Blade separation

- Keep Blade templates presentation-only.
- Do not put business logic in Blade.
- Do not use raw PHP beyond simple conditionals or loops.

### JavaScript organization

- Use separate, clearly named functions.
- Use comment markers to separate major sections.
- Avoid inline anonymous functions for major logic blocks.

Comment marker examples:

```js
// ==================== LOAD DATA ====================
// ==================== FORM SUBMIT ====================
// ==================== DELETE HANDLER ====================
```

### Tables

- Render rows with `@foreach`.
- Avoid hardcoded table rows.
- Handle empty states with `@forelse` and `@empty`.

### Modals

- Show a loading spinner inside modals while AJAX-loaded data is being fetched.

### View modification rule

- For existing views, provide only modified blocks.
- Provide the full file only for newly created views.

## Routes

### Naming

- Use descriptive REST-style route names.
- Format route names as `{resource}.{action}`.

Examples:

- `users.index`
- `users.store`
- `users.update`
- `users.destroy`

### Synchronization

- Keep routes synchronized with controller methods.
- Ensure every route maps to a matching controller method.
- Remove or update routes immediately when controller methods change.
- Use route model binding where it improves readability and reduces manual lookup code.

## Migrations and file creation

### Terminal requirement

- Always use terminal and Artisan commands for Laravel file creation.
- Do not manually create files that Artisan should generate.

Commands:

- migration: `php artisan make:migration {migration_name}`
- model: `php artisan make:model {ModelName}`
- controller: `php artisan make:controller {ControllerName}`
- request: `php artisan make:request {RequestName}`
- seeder: `php artisan make:seeder {SeederName}`
- factory: `php artisan make:factory {FactoryName}`

Preference:

- generate `FormRequest` classes for non-trivial validation flows
- keep generated namespaces and default Laravel structure intact

### Deliverable requirements

When providing instructions that involve file creation, always include:

- the exact Artisan command used
- the resulting file path after generation

### Best-practice rationale

- keeps naming and namespaces consistent
- reduces human error
- ensures proper class structure

## Code delivery rules

### Adding new code

- Provide the full file for all newly created files, including:
  - models
  - controllers
  - views
  - migrations
  - request classes
  - any other newly generated file

### Modifying existing code

- Provide only the modified blocks.
- Identify the modified function or section clearly.
- Include surrounding context lines only when needed.
- When working directly in the repository, make the edits in place and summarize the changed files clearly.

### Simplification

- Prefer simple, clean, optimized code.
- Avoid deep nesting and over-engineering.
- Choose simple working solutions over clever complexity.

### Fixes and modifications

- Provide exactly what was requested.
- Do not suggest alternatives unless asked.
- Do not add optional solutions unless asked.

## General coding style

### Standards

- Follow PSR-12.

### Naming conventions

- variables: `camelCase`
- methods: `camelCase`
- classes: `PascalCase`
- models: `PascalCase` with `Model` suffix
- database tables: `snake_case` plural
- database columns: `snake_case`

### Documentation

- Add docblocks for all classes, methods, and complex properties.
- Use `@param`, `@return`, and `@throws` where applicable.

### Security

- Validate all user input before processing.
- Never trust raw user input.
- Use Laravel built-in validation, authorization, casting, escaping, and storage tools.

### Code quality

- Write clean, simple, readable code.
- Avoid redundant logic.
- Keep methods focused on a single responsibility.
- Use descriptive variable and method names.
- Use eager loading when rendering related data to avoid N+1 query issues.
- Use pagination for large listing pages instead of loading everything at once.

### File uploads

- Validate uploaded files by type, size, and required presence.
- Store uploads using Laravel's storage APIs instead of manual path handling.
- Use predictable storage locations and filenames that avoid collisions.
- Clean up or replace obsolete files when updates remove the old asset.

### Logging and failures

- Return user-friendly error messages in the UI.
- Log unexpected exceptions when the application needs diagnostic visibility.

### Soft deletes

- Use soft deletes when records should remain recoverable or auditable.

### Anti-patterns to avoid

- Do not place business logic in Blade templates.
- Do not use raw SQL for normal CRUD flows when Eloquent or the query builder is sufficient.
- Do not duplicate validation rules across multiple layers without reason.
- Do not leave routes and controller methods out of sync.
