> public Intervention\Validation\Rules\Isin::__construct()

Checks for a valid [International Securities Identification Number](https://en.wikipedia.org/wiki/International_Securities_Identification_Number) (ISIN).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\Isin;

$validator = Validator::make($request->all(), [
    'my-value' => new Isin(),
]);
```


