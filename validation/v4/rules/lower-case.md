---
title: "Lower Case Rule"
subtitle: "Validate a String in Lower Case"
lead: "Discover how to validate lower case strings with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Lowercase::__construct()

The given value must be all lower case letters.

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Lowercase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Lowercase(),
]);
```


