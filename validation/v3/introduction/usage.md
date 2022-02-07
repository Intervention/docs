# Usage
## Basic Usage of Intervention Validation

[TOC]

## Usage with Laravel Framework

The Validation library is built to work with the Laravel Framework and provides over 30 additional validation rules including error messages. You can use this rules in combination with Laravel's rules by passing them to the validator.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\HexColor;

$validator = Validator::make($request->all(), [
    'color' => new Hexcolor(3), // pass rule as object
    'number' => ['required', 'creditcard'], // or pass rule as string
    'name' => 'required|min:3|max:20|username', // combining rules works as well
]);
```

### Customizing error messages

Add the corresponding key to `/resources/lang/<language>/validation.php` like this:

```php
// example
'iban' => 'Please enter IBAN number!',
```

Or add your custom messages directly to the validator like described in the [Laravel docs](https://laravel.com/docs/8.x/validation#manual-customizing-the-error-messages).


## Standalone Usage

It is also possible to use this library without the Laravel framework. You won't have the Laravel facades available, so make sure to use `Intervention\Validation\Validator` for your calls.

### Example

```php
use Intervention\Validation\Validator;
use Intervention\Validation\Rules\Creditcard;
use Intervention\Validation\Exceptions\ValidationException;

// use static factory method to create laravel validator
$validator = Validator::make($request->all(), [
    'ccnumber' => new Creditcard(),
    'iban' => ['required', 'iban'],
    'color' => 'required|hexcolor:3',
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
