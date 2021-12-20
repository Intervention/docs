# Upper Case Rule
## Validate string formated in upper case

> public Intervention\Validation\Rules\Uppercase::__construct()

The field under validation must be all upper case.

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Uppercase;

$validator = Validator::make($request->all(), [
    'my-value' => new Uppercase(),
]);
```