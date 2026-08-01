---
title: "Data URI Rule"
subtitle: "Validate Data URI scheme string"
lead: "Validate Data URI scheme strings in Laravel with Intervention Validation. Check Base64 data URIs format."
sort: 9
---

> public Intervention\Validation\Rules\DataUri::__construct(?array $media_types = null)

The field under validation must be a valid [Data URI](https://en.wikipedia.org/wiki/Data_URI_scheme).

### Parameters

#### media_types (optional)

Parameter to determine the media type to be validated. Can either be `null` to
allow all valid media types or an array of allowed types.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\DataUri;

$validator = Validator::make($request->all(), [
    'attribute-key' => new DataUri(),
]);
```

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\DataUri;

$validator = Validator::make($request->all(), [
    'attribute-key' => new DataUri([
        'image/jpeg',
        'image/png',
    ]),
]);
```
