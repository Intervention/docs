---
title: "ISSN Rule"
subtitle: "Validate International Standard Serial Number"
lead: "Explore how to validate International Standard Serial Numbers (ISSN) with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Issn::__construct()

Checks for a valid [International Standard Serial Number](https://en.wikipedia.org/wiki/International_Standard_Serial_Number) (ISSN).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Issn;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Issn(),
]);
```


