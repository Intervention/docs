---
title: "ULID Rule"
subtitle: "Validate a Universally Unique Lexicographically Sortable Identifier"
sort: 26
---

> public Intervention\Validation\Rules\Ulid::__construct()

The field under validation must be a valid [Universally Unique Lexicographically Sortable Identifier](https://github.com/ulid/spec).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Ulid;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Ulid(),
]);
```
