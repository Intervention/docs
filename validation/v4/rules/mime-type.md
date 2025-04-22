---
title: "Media (MIME) Type Rule"
subtitle: "Validate MIME Type Strings"
lead: "Explore how to validate mime type strings with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\MimeType::__construct()

Checks for a valid [Mime Type](https://en.wikipedia.org/wiki/Media_type) (Media type).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\MimeType;

$validator = Validator::make($request->all(), [
    'attribute-key' => new MimeType(),
]);
```


