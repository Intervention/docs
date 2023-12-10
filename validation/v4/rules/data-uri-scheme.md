# Data URI Rule
## Validate Data URI scheme string

> public Intervention\Validation\Rules\DataUri::__construct(?array $media_types = null)

The field under validation must be a valid [Data URI](https://en.wikipedia.org/wiki/Data_URI_scheme).

### Parameters

#### media_types (optional)

Parameter to determine the media type to be validated. Can either be `null` to
allow all valid media types or an array of allowed types.

### Example

```php
use Intervention\Validation\Rules\DataUri;

$validator = Validator::make($request->all(), [
    'attribute-key' => new DataUri(),
]);
```

```php
use Intervention\Validation\Rules\DataUri;

$validator = Validator::make($request->all(), [
    'attribute-key' => new DataUri([
        'image/jpeg',
        'image/png',
    ]),
]);
```
