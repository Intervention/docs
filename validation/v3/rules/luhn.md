# Luhn Rule
## Validate a string against Luhn algorithm

> public Intervention\Validation\Rules\Luhn::__construct()

The given value must verify against its included [Luhn algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm) check digit.

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Luhn;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Luhn(),
]);
```


