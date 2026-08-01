---
title: "Camel Case Rule"
subtitle: "Validate Camel Case String"
lead: "Validate camelCase strings in Laravel with Intervention Validation. Ensure proper camelCase formatting."
sort: 4
---

> public Intervention\Validation\Rules\Camelcase::__construct()

The field under validation must be formatted in [Camel case](https://en.wikipedia.org/wiki/Camel_case).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Camelcase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Camelcase(),
]);
```
