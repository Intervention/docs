---
title: "CIDR Rule"
subtitle: "Validate Classless Inter-Domain Routing string"
lead: "Validate CIDR notation (Classless Inter-Domain Routing) in Laravel with Intervention Validation. IP range checks."
sort: 5
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
