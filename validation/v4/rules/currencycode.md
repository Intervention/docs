---
title: "Currency Code"
subtitle: "Validate ISO 4217 Currency Codes"
lead: "Validate ISO 4217 currency codes in Laravel with Intervention Validation. International currency checks."
sort: 8
---

> public Intervention\Validation\Rules\CurrencyCode::__construct(string $format = CurrencyCode::ALPHA, bool $strict = true)

The field under validation must be a valid [currency code](https://en.wikipedia.org/wiki/ISO_4217) according to ISO 4217.

#### Parameters

**format**

The currency code has two different formats `CurrencyCode::ALPHA` or `CurrencyCode::NUMERIC`. Select the format you want to check. Default `CurrencyCode::ALPHA`.

**strict**

If `strict` is `true`, the code must be passed in uppercase. Otherwise, the case doesn't matter.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\CurrencyCode;

$validator = Validator::make($request->all(), [
    'attribute-key' => new CurrencyCode(),
]);
```
