The Validation library is built to work with the Laravel Framework and provides over 30 additional validation rules including error messages. You can use this rules in combination with Laravel's rules by passing them to the validator.

## Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Creditcard;
use Intervention\Validation\Rules\HexColor;
use Intervention\Validation\Rules\Username;

$validator = Validator::make($request->all(), [
    'color' => new Hexcolor(3), // pass rule as object
    'name' => ['required', 'min:3', 'max:20', new Username()], // combining rules works as well
]);
```

**Make sure to pass any of the additional validation rules as objects and not as strings.**

### Customizing error messages

Add the corresponding key to `/resources/lang/<language>/validation.php` like this:

```php
// example
'iban' => 'Please enter IBAN number!',
```

Or add your custom messages directly to the validator like described in the [Laravel docs](https://laravel.com/docs/8.x/validation#manual-customizing-the-error-messages).

