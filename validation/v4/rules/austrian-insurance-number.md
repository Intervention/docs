---
title: "Austrian Insurance Number Rule"
subtitle: "Validate the Austria Social Insurance Number"
lead: "Validate Austrian Social Insurance Numbers in Laravel with Intervention Validation. Austrian-specific validation rule."
sort: 1
---

> public Intervention\Validation\Rules\AustrianInsuranceNumber::__construct()

Checks for a valid [Austrian social insurance number](https://de.wikipedia.org/wiki/Sozialversicherungsnummer#%C3%96sterreich).

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\AustrianInsuranceNumber;

// validate GTIN
$validator = Validator::make($request->all(), [
    'attribute-key' => new AustrianInsuranceNumber(),
]);
```
