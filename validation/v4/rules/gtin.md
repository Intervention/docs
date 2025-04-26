---
title: "GTIN Rule"
subtitle: "Validate a Global Trade Item Number"
lead: "Learn how to validate the Global Trait Item Numbers (GTIN) with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Gtin::__construct(array $lengths = [8, 12, 13, 14])

Checks for a valid [Global Trade Item Number](https://en.wikipedia.org/wiki/Global_Trade_Item_Number).

### Parameters

#### lengths (optional)

Optional array of allowed lengths to check only for certain types (GTIN-8, GTIN-12, GTIN-13 or GTIN-14).

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Gtin;

// validate GTIN
$validator = Validator::make($request->all(), [
    'attribute-key' => new Gtin(),
]);
```

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Gtin;

// validate GTIN-8 or GTIN-12
$validator = Validator::make($request->all(), [
    'attribute-key' => new Gtin([8, 12]),
]);
```

