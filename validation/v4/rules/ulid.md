---
title: "ULID Rule"
subtitle: "Validate a Universally Unique Lexicographically Sortable Identifier"
lead: "Validate ULID (Universally Unique Lexicographically Sortable Identifier) in Laravel with Intervention Validation. ULID format checks."
sort: 34
---

> public Intervention\Validation\Rules\Ulid::__construct()

The field under validation must be a valid [Universally Unique Lexicographically Sortable Identifier](https://github.com/ulid/spec).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Ulid;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Ulid(),
]);
```
