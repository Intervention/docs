# Media (MIME) type Rule
## Validate MIME type strings

> public Intervention\Validation\Rules\MimeType::__construct()

Checks for a valid [Mime Type](https://en.wikipedia.org/wiki/Media_type) (Media type).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\MimeType;

$validator = Validator::make($request->all(), [
    'my-value' => new MimeType(),
]);
```


