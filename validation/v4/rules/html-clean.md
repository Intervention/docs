---
title: "HTML Clean Rule"
subtitle: "Validate if Text is Free of any HTML Tags"
lead: "Validate HTML-free strings in Laravel with Intervention Validation. Ensure no HTML tags in user input."
sort: 15
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


