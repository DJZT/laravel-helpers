# Laravel Helpers

**English** · [Українська](README.uk.md)

One `require` that pulls in every DJZT Laravel helper package.

```bash
composer require djzt/laravel-helpers
```

This is a Composer **metapackage**: it ships no code of its own, only the list of
packages below. Every provider is auto-discovered, so there is nothing to register.

## What you get

| Package | What it does | Docs |
| --- | --- | --- |
| [`djzt/laravel-request-helper`](https://github.com/DJZT/laravel-request-helper) | Typed request accessors — `nullable*`, `optional*` and `required*`, with an explicit `Optional` marker that keeps "key absent", "null" and "0" apart | [README](https://github.com/DJZT/laravel-request-helper#readme) |
| [`djzt/laravel-resource-helper`](https://github.com/DJZT/laravel-resource-helper) | Helpers for API Resources — one config-driven date format across the API, plus money, numbers, enums, files and conditional attributes | [README](https://github.com/DJZT/laravel-resource-helper#readme) |

```php
// djzt/laravel-request-helper
$request->requiredInteger('qty');   // int               — 422 if absent, null or uncastable
$request->optionalString('name');   // string|null|Optional

// djzt/laravel-resource-helper
'created_at' => $this->date($this->created_at),   // "2026-09-01"
'price'      => $this->money($this->price),       // "1999.50"
```

Requires PHP 8.2+ and Laravel 12 or 13.

## Only want one of them?

Require it directly — the packages are independent and neither depends on this one:

```bash
composer require djzt/laravel-request-helper
```

Installing the metapackage alongside an individual package is harmless; Composer
resolves them to the same install.

## Adding a helper to the set

1. Publish the new package on its own (its own repository, its own tags, Packagist).
2. Add it to `require` here, with a `^` constraint on its first stable minor.
3. Tag a new minor of this metapackage.

Because a metapackage contains nothing but its `require` block, that is the whole
release: existing installs pick the new helper up on the next `composer update`.

## Versioning

The metapackage is versioned on its own, independently of the packages it points at.
A new helper, or a constraint widened to a new minor of an existing helper, is a
minor release here; dropping a package from the set is a major one.

## License

MIT. See [LICENSE](LICENSE).
