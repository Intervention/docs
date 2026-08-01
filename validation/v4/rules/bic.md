---
title: "BIC Rule"
subtitle: "Validate a Business Identifier Code"
lead: "Validate Business Identifier Codes (BIC/SWIFT) in Laravel with Intervention Validation. Banking code validation."
sort: 3
---

> public Intervention\Validation\Rules\Bic::__construct()

Checks if the field under validation is a valid [Business Identifier Code](https://en.wikipedia.org/wiki/ISO_9362) (BIC).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Bic;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Bic(),
]);
```
