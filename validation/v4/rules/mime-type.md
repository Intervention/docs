---
title: "Media (MIME) Type Rule"
subtitle: "Validate MIME Type Strings"
lead: "Validate MIME type strings in Laravel with Intervention Validation. Content type format checks."
sort: 28
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


