# Intervention Validation
## Missing Laravel Validation Rules

Intervention Validation is an extension library for Laravel's own validation
system. The package adds over 30 additional validation rules to verify data
like IBAN, BIC, ISBN, creditcard numbers and more.

- All rules implement the `Illuminate\Contracts\Validation\ValidationRule` interface
- Use the additional rules in combination with Laravel's own rules

### Installation

You can install this package quick and easy with Composer.

Require the package via Composer:

```bash
composer require intervention/validation
```

The Validation library is built to work with the Laravel Framework (>=10). It
comes with a service provider, which will be discovered automatically and
registers the validation rules into your installation.

### Usage with Laravel Framework

The Validation library is built to work with the Laravel Framework and provides
over 30 additional validation rules including error messages. You can use this
rules in combination with Laravel's rules by passing them to the validator.

#### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Hexadecimalcolor;

$validator = Validator::make($request->all(), [
    'color' => new Hexadecimalcolor(3), // pass rule as object
    'number' => ['required', 'creditcard'], // or pass rule as string
    'name' => 'required|min:3|max:20|username', // combining rules works as well
]);
```

#### Customizing Error Messages

Add the corresponding key to `/resources/lang/<language>/validation.php` like this:

```php
'iban' => 'Please enter IBAN number!',
```

Or add your custom messages directly to the validator like [described in the docs](https://laravel.com/docs/10.x/validation#manual-customizing-the-error-messages).
