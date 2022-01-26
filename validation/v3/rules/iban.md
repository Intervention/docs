# IBAN Clean Rule
## Validate International Bank Account Numbers

> public Intervention\Validation\Rules\Iban::__construct()

Checks for a valid [International Bank Account Number](https://en.wikipedia.org/wiki/International_Bank_Account_Number) (IBAN).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Iban;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Iban(),
]);
```


