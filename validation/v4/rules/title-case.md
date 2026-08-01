---
title: "Title Case Rule"
subtitle: "Validate String Formatted in Title Case"
lead: "Validate Title Case strings in Laravel with Intervention Validation. Ensure proper title case format."
sort: 33
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
