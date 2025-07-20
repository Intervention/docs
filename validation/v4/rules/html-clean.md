---
title: "HTML Clean Rule"
subtitle: "Validate if Text is Free of any HTML Tags"
lead: "Learn how to validate that strings are free of any HTML code with the additional validation rules of Intervention Validation for your Laravel application."
sort: 12
---

> public Intervention\Validation\Rules\HtmlClean::__construct()

The field under validation must be free of any html code.

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\HtmlClean;

$validator = Validator::make($request->all(), [
    'attribute-key' => new HtmlClean(),
]);
```


