---
title: "Lower Case Rule"
subtitle: "Validate a String in Lower Case"
---

> public Intervention\Validation\Rules\Lowercase::__construct()

The given value must be all lower case letters.

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Lowercase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Lowercase(),
]);
```


