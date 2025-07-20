---
title: "IMEI Rule"
subtitle: "Validate International Mobile Equipment Identity "
sort: 12
---

> public Intervention\Validation\Rules\Imei::__construct()

The field under validation must be a [International Mobile Equipment Identity](https://en.wikipedia.org/wiki/International_Mobile_Equipment_Identity) (IMEI).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Imei;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Imei(),
]);
```
