---
title: "Country Code"
subtitle: "Validate ISO-3166 Country Codes"
lead: "Learn how to validate ISO-3166 Country Codes with the additional validation rules of Intervention Validation for your Laravel application."
sort: 6
---

> public Intervention\Validation\Rules\CountryCode::__construct(string $format = CountryCode::ALPHA2, bool $strict = true)

The field under validation must be a valid [country code](https://en.wikipedia.org/wiki/ISO_3166-1) according to ISO 3166-1.

### Parameters

**format**

The country code has three different formats `CountryCode::ALPHA2`, `CountryCode::ALPHA3` or `CountryCode::NUMERIC`. Select the format you want to check. Default `CountryCode::ALPHA2`.

**strict**

If `strict` is `true`, the language code must be passed in uppercase. Otherwise, the case doesn't matter.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\CountryCode;

$validator = Validator::make($request->all(), [
    'attribute-key' => new CountryCode(),
]);
```
