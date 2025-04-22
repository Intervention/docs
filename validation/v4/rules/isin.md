---
title: "ISIN Rule"
subtitle: "Validate International Securities Identification Number"
lead: "Discover how to validate International Securities Identification Numbers (ISIN) with the additional validation rules of Intervention Validation for your Laravel application."
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


