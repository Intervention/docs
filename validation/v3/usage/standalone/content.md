It is also possible to use this library without the Laravel framework. You won't have the Laravel facades available, so make sure to use `Intervention\Validation\Validator` for your calls.

## Example

```php
use Intervention\Validation\Validator;
use Intervention\Validation\Rules\Creditcard;
use Intervention\Validation\Exceptions\ValidationException;

// use static factory method to create laravel validator
$validator = Validator::make($request->all(), [
    'ccnumber' => new Creditcard(),
    'iban' => ['required', new Iban()],
]);

// validate single values by calling static methods
$result = Validator::isHexcolor('foobar'); // false
$result = Validator::isHexcolor('#ccc'); // true
$result = Validator::isBic('foo'); // false

// assert single values
try {
    Validator::assertHexcolor('foobar');
} catch (ValidationException $e) {
    $message = $e->getMessage();
}
```
