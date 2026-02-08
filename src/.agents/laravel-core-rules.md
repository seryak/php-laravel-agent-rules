# laravel/core rules

## Follow the Laravel Way

- Use `php artisan make:` commands to create new files (e.g. migrations, controllers, models, etc.).
  You can list available Artisan commands using the `list-artisan-commands` tool.
- If you need to create a generic PHP class, use `php artisan make:class`.
- Always pass the `--no-interaction` flag to all Artisan commands to ensure they work without user input.
  Also pass the correct `--options` to guarantee proper behavior.

## Database

- Always use proper Eloquent relationship methods with explicit return type hints.
  Prefer Eloquent relationships over raw SQL queries or manual joins.
- Before suggesting raw database queries, use Eloquent models and relationships.
- Avoid using `DB::`; prefer direct model calls or `Model::query()` only when justified.
- Generate code that prevents N+1 query problems by using eager loading.
- Use Laravel’s Query Builder for very complex database operations.
- Do NOT use `query()` without a clear necessity.
- If the query does not require dynamic construction (conditions, scopes, joins, etc.),
  call methods directly on the model.

### Example

❌ Bad

```php
Feed::query()
    ->orderBy('title')
    ->get();
```

✅ Good

```php
Feed::orderBy('title')->get();
```

Using `query()` is allowed only when:
- conditional query building is required;
- complex branching logic is involved;
- the query builder needs to be passed between methods.

## Model Creation

- When creating new models, ALWAYS ask whether factories and seeders should also be created.
- If necessary, clarify with the user whether additional related artifacts are required,
  using `list-artisan-commands` to check the available options for `php artisan make:model`.

## API & Eloquent Resources

- When developing APIs, default to using Eloquent API Resources and API versioning.
- If existing API routes do not follow this approach, adhere to the current application conventions.

## Controllers & Validation

- ALWAYS create Form Request classes for validation instead of inline validation in controllers.
- Validation MUST be encapsulated in the `rules()` method.
- Include both validation rules and custom error messages.
- Check sibling Form Request classes to determine whether the application uses
  array-based or string-based validation rules.
- StoreRequest and UpdateRequest often duplicate most rules except for a few fields.
  Do NOT duplicate rules; use inheritance and override only the differing fields.

## Views

- When passing variables to views, ALWAYS use `compact()` when possible.

❌ Bad

```php
return view('feeds.index', [
    'feeds' => $feeds,
]);
```

✅ Good

```php
return view('feeds.index', compact('feeds'));
```

## Queues

- Use queued jobs with the `ShouldQueue` interface for long-running operations.

## Authentication & Authorization

- Use Laravel’s built-in authentication and authorization features
  (gates, policies, Sanctum, etc.).

## URL Generation

- When generating links to other pages, prefer named routes and the `route()` function.

## Configuration

- Use environment variables only in configuration files.
- NEVER call `env()` directly outside of config files.
- Always use `config('app.name')` instead of `env('APP_NAME')`.

## Testing

- When creating models for tests, use model factories.
- Before manually configuring a model, check whether the factory provides reusable custom states.
- Faker: use `$this->faker` or `fake()` consistently with existing project conventions.
- Use `php artisan make:test [options] {name}` for feature tests.
- Pass `--unit` only when a unit test is explicitly required.
- Most tests should be feature tests.

## Vite Error

- If you encounter the error:

  `Illuminate\Foundation\ViteException: Unable to locate file in Vite manifest`

  Run `npm run build`, or ask the user to run `npm run dev` or `composer run dev`.

## Laravel 12

- Use the `search-docs` tool to get version specific documentation.
- Since Laravel 11, Laravel has a new streamlined file structure which this project uses.

### Laravel 12 Structure
- No middleware files in `app/Http/Middleware/`.
- `bootstrap/app.php` is the file to register middleware, exceptions, and routing files.
- `bootstrap/providers.php` contains application specific service providers.
- **No app\Console\Kernel.php** - use `bootstrap/app.php` or `routes/console.php` for console configuration.
- **Commands auto-register** - files in `app/Console/Commands/` are automatically available and do not require manual registration.

### Database
- When modifying a column, the migration must include all of the attributes that were previously defined on the column. Otherwise, they will be dropped and lost.
- Laravel 11 allows limiting eagerly loaded records natively, without external packages: `$query->latest()->limit(10);`.

### Models
- Casts can and likely should be set in a `casts()` method on a model rather than the `$casts` property. Follow existing conventions from other models.

## Laravel Pint Code Formatter

- You must run `vendor/bin/pint --dirty` before finalizing changes to ensure your code matches the project's expected style.
- Do not run `vendor/bin/pint --test`, simply run `vendor/bin/pint` to fix any formatting issues.
