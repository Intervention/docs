---
title: "Lower Case Rule"
subtitle: "Validate a String in Lower Case"
lead: "Validate lowercase strings in Laravel with Intervention Validation. Ensure all characters are lowercase."
sort: 26
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


