---
title: "JWT Rule"
subtitle: "Validate a JSON Web Token"
lead: "Validate JSON Web Token (JWT) format in Laravel with Intervention Validation. JWT structure checks."
sort: 22
---

> public Intervention\Validation\Rules\Jwt::__construct()

The value under validation must be in the format of a [JSON Web Token](https://en.wikipedia.org/wiki/JSON_Web_Token).

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


