---
title: "ULID Rule"
subtitle: "Validate a Universally Unique Lexicographically Sortable Identifier"
lead: "Learn how to validate the Universally Unique Lexicographically Sortable Identifier (ULID) format with the additional validation rules of Intervention Validation for your Laravel application."
sort: 29
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
