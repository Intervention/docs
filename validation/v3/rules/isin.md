---
title: "ISIN Rule"
subtitle: "Validate International Securities Identification Number"
sort: 14
---

> public Intervention\Validation\Rules\Isin::__construct()

Checks for a valid [International Securities Identification Number](https://en.wikipedia.org/wiki/International_Securities_Identification_Number) (ISIN).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Isin;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Isin(),
]);
```


