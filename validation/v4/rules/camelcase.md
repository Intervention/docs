---
title: "Camel Case Rule"
subtitle: "Validate Camel Case String"
lead: "Explore how to validate camel case strings with the additional validation rules of Intervention Validation for your Laravel application."
sort: 3
---

> public Intervention\Validation\Rules\Camelcase::__construct()

The field under validation must be a formated in [Camel case](https://en.wikipedia.org/wiki/Camel_case).

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
