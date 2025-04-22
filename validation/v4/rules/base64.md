---
title: "Base64 Rule"
subtitle: "Validate a Base64 Encoded String"
lead: "Discover how to validate Base64 encoded strings with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Base64::__construct()

The field under validation must be [Base64 encoded](https://en.wikipedia.org/wiki/Base64).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Base64;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Base64(),
]);
```
