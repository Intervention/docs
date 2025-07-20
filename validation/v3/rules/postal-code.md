---
title: "Postal Code Rule"
subtitle: "Validate Postal Codes for Individual Countries"
sort: 21
---

> public Intervention\Validation\Rules\Postalcode::__construct(string $countrycode)

The field under validation must be a [postal code](https://en.wikipedia.org/wiki/Postal_code) of the given country.

### Parameters

#### countrycode

Country code string in [ISO-639-1](https://en.wikipedia.org/wiki/ISO_639-1) format.

### Example

```php
use Intervention\Validation\Rules\Postalcode;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Postalcode('de'),
]);
```
