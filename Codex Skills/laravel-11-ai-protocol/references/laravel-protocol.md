# Laravel 11 Protocol Reference

Use this file as the detailed rules reference for the `laravel-11-ai-protocol` skill.

## Table of contents

- [Execution gate](#execution-gate)
- [Database rules](#database-rules)
- [Models](#models)
- [Controllers](#controllers)
- [Services and actions](#services-and-actions)
- [Views](#views)
- [Routes](#routes)
- [API resources](#api-resources)
- [Performance and async work](#performance-and-async-work)
- [Testing](#testing)
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
- Use `FormRequest` classes by default for `store` and `update` actions.
- Reserve inline `$request->validate()` for very small or exceptional cases.
- Apply specific validation rules per field.
- Avoid vague validation messages.
- Provide clear, user-friendly custom messages.
- Use SweetAlert2 to show validation errors and alerts to the user.
- Use the `authorize()` method inside `FormRequest` when request-level authorization is appropriate.
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

### Authorization

- Use Laravel Policies by default for resource-based authorization.
- Keep authorization checks close to the resource action by using controller helpers such as `authorize()` and `authorizeResource()` where appropriate.
- Use Gates or middleware for broader application access rules when Policies are not the right fit.
- Avoid scattering custom permission logic across unrelated controllers or views.

## Services and actions

### Business workflow separation

- Use service classes or action classes for multi-step business workflows.
- Keep controllers focused on request handling, validation flow, authorization, and response formatting.
- Keep models focused on relationships, casts, scopes, and small domain helpers.
- Do not place large business processes directly inside controllers, models, or Blade templates.

### Typical use cases

- Use services/actions for workflows such as:
  - create/update flows with related records
  - inventory adjustments
  - payment or billing steps
  - approval flows
  - import/export orchestration
  - any process with side effects or multiple persistence steps

### Transaction boundaries

- Wrap service/action workflows in `DB::transaction()` when partial completion would leave inconsistent state.
- Keep transaction scope as small as practical while still preserving integrity.

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
- Use route model binding by default when resolving Eloquent models from route parameters.
- Avoid manual `find()` or `findOrFail()` lookups in controllers when route model binding can express the intent cleanly.

## API resources

### JSON response formatting

- Use Laravel API Resources for structured JSON responses beyond very simple success/error AJAX payloads.
- Keep response shaping out of controllers when returning model data or collections.
- Use API Resources to standardize field names, nested relationships, and conditional attributes.
- Avoid returning raw model instances directly for public-facing APIs unless the response is intentionally trivial.

### Consistency

- Keep API response formats consistent across related endpoints.
- Use dedicated resource classes for single-item and collection responses when helpful.

## Performance and async work

### Queue slow tasks

- Queue slow or non-blocking work such as:
  - emails
  - notifications
  - imports and exports
  - report generation
  - media processing
  - third-party API follow-up tasks
- Keep HTTP requests fast by offloading background work to queues when the user does not need an immediate inline result.

### Cache expensive reads

- Cache expensive read-heavy queries and computed aggregates when the data is reused frequently.
- Consider caching for dashboards, settings, lookup lists, report summaries, and other repeated reads.
- Invalidate or refresh cache entries deliberately when write operations change the underlying data.
- Do not add caching blindly to highly dynamic queries without a clear invalidation strategy.

### Query efficiency

- Use eager loading intentionally to avoid N+1 query issues.
- Select only the needed columns for heavier queries when practical.
- Extract repeated filters into local scopes or query objects when the same query logic appears in multiple places.

## Testing

### Feature tests

- Add Feature tests for new features by default.
- Add regression-oriented Feature tests for bug fixes when practical.
- Prefer Feature tests for request/response flows, authorization checks, validation behavior, and database side effects.

### Unit tests

- Add Unit tests for isolated domain or helper logic when the behavior is complex enough to benefit from focused coverage.
- Keep test intent clear and aligned with the behavior being protected.

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
- Prefer Policies for resource authorization and `FormRequest` classes for request validation and request-level authorization.

### Code quality

- Write clean, simple, readable code.
- Avoid redundant logic.
- Keep methods focused on a single responsibility.
- Use descriptive variable and method names.
- Use eager loading when rendering related data to avoid N+1 query issues.
- Use pagination for large listing pages instead of loading everything at once.
- Use services/actions for multi-step workflows, API Resources for structured JSON, queues for slow tasks, and caching for expensive repeated reads when appropriate.

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
