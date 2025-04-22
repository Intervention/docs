---
title: "Luhn Rule"
subtitle: "Validate a String Against Luhn Algorithm"
lead: "Learn how to validate strings agains the Luhn Algorithm with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Luhn::__construct()

The given value must verify against its included [Luhn algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm) check digit.

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Luhn;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Luhn(),
]);
```


