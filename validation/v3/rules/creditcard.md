# Creditcard Rule
## Validate Creditcard Numbers

> public Intervention\Validation\Rules\Creditcard::__construct()

The field under validation must be a valid [creditcard number](https://en.wikipedia.org/wiki/Payment_card_number).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Creditcard;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Creditcard(),
]);
```
