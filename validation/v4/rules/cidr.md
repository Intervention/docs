---
title: "CIDR Rule"
subtitle: "Validate Classless Inter-Domain Routing string"
lead: "Discover how to validate Classless Inter-Domain Routing notations (CIDR) with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Cidr::__construct()

Check if the field under validation is a [Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) notation (CIDR).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Cidr;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Cidr(),
]);
```
