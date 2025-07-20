---
title: "Austrian Insurance Number Rule"
subtitle: "Validate the Austria Social Insurance Number"
lead: "Explore how to validate the Austrian Social Insurance Number with the additional validation rules of Intervention Validation for your Laravel application."
sort: 0
---

> public Intervention\Validation\Rules\AustrianInsuranceNumber::__construct()

Checks for a valid [austrian social insurance number](https://de.wikipedia.org/wiki/Sozialversicherungsnummer#%C3%96sterreich).

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\AustrianInsuranceNumber;

// validate GTIN
$validator = Validator::make($request->all(), [
    'attribute-key' => new AustrianInsuranceNumber(),
]);
```
