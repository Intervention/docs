---
title: "Kebab Case Rule"
subtitle: "Validate a String in Kebab Case"
lead: "Discover how to validate strings in Kebab Case with the additional validation rules of Intervention Validation for your Laravel application."
sort: 20
---

> public Intervention\Validation\Rules\Kebabcase::__construct()

The value under validation must be formated in [Kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Kebabcase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Kebabcase(),
]);
```


