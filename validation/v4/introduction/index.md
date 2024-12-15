# Intervention Validation
## Missing Laravel Validation Rules
Enhance Laravel validation system seamlessly with Intervention Validation, offering 30+ additional validation rules like IBAN, ISBN, postal codes and credit card checks.

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

The Validation library is built to work with [Laravel's
Validation Framework](https://laravel.com/docs/11.x/validation) and provides over 30
additional validation rules including error messages. You can use this rules in
combination with Laravel's rules by passing them to the validator.

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
Laravel docs](https://laravel.com/docs/11.x/validation#customizing-the-error-messages).
