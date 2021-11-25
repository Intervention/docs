# Base64 Rule
## Validate a base64 encoded string

> public Intervention\Validation\Rules\Base64 __construct()

The field under validation must be [Base64 encoded](https://en.wikipedia.org/wiki/Base64).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\Base64;

$validator = Validator::make($request->all(), [
    'my-value' => new Base64(),
]);
```
