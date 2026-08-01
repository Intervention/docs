---
title: "IMEI Rule"
subtitle: "Validate International Mobile Equipment Identity "
lead: "Validate International Mobile Equipment Identifier (IMEI) in Laravel with Intervention Validation. Device checks."
sort: 17
---

> public Intervention\Validation\Rules\Imei::__construct()

The field under validation must be an [International Mobile Equipment Identity](https://en.wikipedia.org/wiki/International_Mobile_Equipment_Identity) (IMEI).

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
