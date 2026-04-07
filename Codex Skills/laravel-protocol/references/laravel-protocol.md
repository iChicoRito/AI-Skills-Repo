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
  - follow Laravel coding standards strictly
  - follow naming conventions strictly
  - avoid deviating from the instructions

## Database rules

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

- Prefer direct SQL queries for small structural changes such as:
  - adding columns
  - dropping columns
  - altering field types or attributes
- Document all SQL queries clearly with comments.
- Use migrations instead when:
  - changes affect multiple environments
  - changes must be version-controlled
  - changes are complex or involve multiple tables

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
- Apply specific validation rules per field.
- Avoid vague validation messages.
- Provide clear, user-friendly custom messages.
- Use SweetAlert2 to show validation errors and alerts to the user.

### AJAX integration

- Use jQuery + AJAX for all form submissions.
- Return JSON responses only.
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

## Views

### UI consistency

- Keep layouts modern, clean, and consistent.
- Preserve the established design system or layout template.

### AJAX form handling

- Use jQuery + AJAX for all form submissions.
- Provide real-time validation feedback.
- Prevent default form submission.
- Display success and error states with SweetAlert2.

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

- Sanitize and validate all user input before processing.
- Never trust raw user input.
- Use Laravel built-in validation and sanitization tools.

### Code quality

- Write clean, simple, readable code.
- Avoid redundant logic.
- Keep methods focused on a single responsibility.
- Use descriptive variable and method names.
