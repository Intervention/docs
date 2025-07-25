---
title: "Snake Case Rule"
subtitle: "Validate String Formated in Snake Case"
lead: "Discover how to validate strings formated in snake case with the additional validation rules of Intervention Validation for your Laravel application."
sort: 27
---

> public Intervention\Validation\Rules\Snakecase::__construct()

The field under validation must formated as [Snake case](https://en.wikipedia.org/wiki/Snake_case) text.

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Snakecase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Snakecase(),
]);
```
