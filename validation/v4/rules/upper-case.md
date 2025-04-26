---
title: "Upper Case Rule"
subtitle: "Validate String Formated in Upper Case"
lead: "Discover how to validate strings in upper case format with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Uppercase::__construct()

The field under validation must be all upper case.

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Uppercase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Uppercase(),
]);
```
