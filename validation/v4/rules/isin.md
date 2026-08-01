---
title: "ISIN Rule"
subtitle: "Validate International Securities Identification Number"
lead: "Validate International Securities Identification Numbers (ISIN) in Laravel with Intervention Validation. Stock codes."
sort: 18
---

> public Intervention\Validation\Rules\Isin::__construct()

Checks for a valid [International Securities Identification Number](https://en.wikipedia.org/wiki/International_Securities_Identification_Number) (ISIN).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Isin;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Isin(),
]);
```


