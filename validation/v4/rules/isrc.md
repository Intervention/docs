---
title: "ISRC Rule"
subtitle: "Validate International Standard Recording Codes"
lead: "Validate International Standard Recording Codes (ISRC) in Laravel with Intervention Validation. Music industry IDs."
sort: 21
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
