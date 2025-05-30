---
title: "Intervention Validation"
label: "Introduction"
subtitle: "Missing Laravel Validation Rules"
lead: "Enhance Laravel's validation system seamlessly with Intervention Validation, offering 30+ additional validation rules like IBAN, ISBN, postal codes, credit card checks and more."
sort: 0
---

- Over 30 additional validations rules for Laravel's validator
- Including error messages in 11 different languages
- All rules implement the `Illuminate\Contracts\Validation\ValidationRule` interface
- Use the additional rules in combination with Laravel's own rules

### Installation

You can install this package quickly and easily with Composer.

```bash
composer require intervention/validation
```

The Validation library is built to work with the Laravel Framework (>=10). It
comes with a service provider, which will be discovered automatically and
registers the validation rules into your installation.

### Use with Laravel Framework

Intervention Validation is built to work with [Laravel's
Validation Framework](https://laravel.com/docs/validation) and provides over 30
additional validation rules including error messages in 11 different languages. 

You can use these rules in combination with Laravel's own rules by passing them to the validator.

#### Example with Controller

```php
use Intervention\Validation\Rules\Hexadecimalcolor;

public function store(Request $request): RedirectResponse
{
    $validated = $request->validate([
        'color' => new Hexadecimalcolor(3), // pass rule as object
        'number' => ['required', 'creditcard'], // or pass rule as string
        'name' => 'required|min:3|max:20|username', // combining rules works as well
    ]);
 
    // The data is valid...
}
```

#### Example with Form Request Validation

```php
use Intervention\Validation\Rules\Hexadecimalcolor;

public function rules(): array
{
    return [
        'color' => new Hexadecimalcolor(3), // pass rule as object
        'number' => ['required', 'creditcard'], // or pass rule as string
        'name' => 'required|min:3|max:20|username', // combining rules works as well
    ];
}
```

#### Example with Manually Created Validator

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Hexadecimalcolor;

$validator = Validator::make($request->all(), [
    'color' => new Hexadecimalcolor(3), // pass rule as object
    'number' => ['required', 'creditcard'], // or pass rule as string
    'name' => 'required|min:3|max:20|username', // combining rules works as well
]);
```

### Customizing Error Messages

Add the corresponding key to `/resources/lang/<language>/validation.php` like this:

```php
'iban' => 'Please enter IBAN number!',
```

Or add your custom messages directly to the validator like [described in the
Laravel docs](https://laravel.com/docs/validation#customizing-the-error-messages).
