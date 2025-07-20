---
title: "IMEI Rule"
subtitle: "Validate International Mobile Equipment Identity "
lead: "Learn how to validate the International Mobile Equipment Identifier format (IMEI) with the additional validation rules of Intervention Validation for your Laravel application."
sort: 14
---

> public Intervention\Validation\Rules\Imei::__construct()

The field under validation must be a [International Mobile Equipment Identity](https://en.wikipedia.org/wiki/International_Mobile_Equipment_Identity) (IMEI).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Imei;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Imei(),
]);
```
