---
title: "VIN Rule"
subtitle: "Validate Vehicle Identification Numbers"
lead: "Validate Vehicle Identification Numbers (VIN) in Laravel with Intervention Validation. Automotive VIN checks."
sort: 37
---

> public Intervention\Validation\Rules\Vin::__construct(bool $checkDigit = false)

The field under validation must be a valid [Vehicle identification number](https://en.wikipedia.org/wiki/Vehicle_identification_number) according to ISO-3779.

### Parameters

**checkDigit**

Optional verification according to the North American check system. Default `false`. Please note that enabling the check digit will cause all VINs without check digit encoded (such as European VIns) to be recognized as invalid, even though they are actually valid.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Vin;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Vin(),
]);
```
