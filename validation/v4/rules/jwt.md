---
title: "JWT Rule"
subtitle: "Validate a JSON Web Token"
lead: "Learn how to validate the JSON Web Token format with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Jwt::__construct()

The value under validation must be a in format of a [JSON Web Token](https://en.wikipedia.org/wiki/JSON_Web_Token).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Jwt;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Jwt(),
]);
```


