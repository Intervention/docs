---
title: "Creditcard Rule"
subtitle: "Validate Credit Card Numbers"
lead: "Validate credit card numbers in Laravel with Intervention Validation. Luhn algorithm and format verification."
sort: 7
---

> public Intervention\Validation\Rules\Creditcard::__construct()

The field under validation must be a valid [credit card number](https://en.wikipedia.org/wiki/Payment_card_number).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Creditcard;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Creditcard(),
]);
```
