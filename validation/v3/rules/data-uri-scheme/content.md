> public Intervention\Validation\Rules\DataUri __construct()

The field under validation must be a valid [Data URI](https://en.wikipedia.org/wiki/Data_URI_scheme).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\DataUri;

$validator = Validator::make($request->all(), [
    'my-value' => new DataUri(),
]);
```
