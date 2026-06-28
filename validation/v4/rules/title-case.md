---
title: "Title Case Rule"
subtitle: "Validate String Formatted in Title Case"
lead: "Explore how to validate strings formatted in title case with the additional validation rules of Intervention Validation for your Laravel application."
sort: 28
---

> public Intervention\Validation\Rules\Titlecase::__construct()

The field under validation must be formatted in [Title case](https://en.wikipedia.org/wiki/Title_case).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Titlecase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Titlecase(),
]);
```
