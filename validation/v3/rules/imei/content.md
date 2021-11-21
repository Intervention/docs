> public Intervention\Validation\Rules\Imei __construct()

The field under validation must be a [International Mobile Equipment Identity](https://en.wikipedia.org/wiki/International_Mobile_Equipment_Identity) (IMEI).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\Imei;

$validator = Validator::make($request->all(), [
    'my-value' => new Imei(),
]);
```


