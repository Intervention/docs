---
title: "ISRC Rule"
subtitle: "Validate International Standard Recording Codes"
lead: "Explore how to validate International Standard Recording Codes with the validation rules of Intervention Validation for your Laravel app."
sort: 17
---

> public Intervention\Validation\Rules\Isrc::__construct()

Checks for a valid [International Standard Recording Code](https://en.wikipedia.org/wiki/International_Standard_Recording_Code).

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Isrc;

// validate code
$validator = Validator::make($request->all(), [
    'attribute-key' => new Isrc(),
]);
```
