---
title: "IBAN Rule"
subtitle: "Validate International Bank Account Numbers"
lead: "Validate International Bank Account Numbers (IBAN) in Laravel with Intervention Validation. Banking checks."
sort: 16
---

> public Intervention\Validation\Rules\Iban::__construct()

Checks for a valid [International Bank Account Number](https://en.wikipedia.org/wiki/International_Bank_Account_Number) (IBAN).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Iban;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Iban(),
]);
```
