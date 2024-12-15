# IBAN Rule
## Validate International Bank Account Numbers
Explore how to validate International Bank Account Numbers (IBAN) with the additional validation rules of Intervention Validation for your Laravel application.

> public Intervention\Validation\Rules\Iban::__construct()

Checks for a valid [International Bank Account Number](https://en.wikipedia.org/wiki/International_Bank_Account_Number) (IBAN).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Iban;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Iban(),
]);
```
