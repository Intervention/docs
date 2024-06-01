# Upper Case Rule
## Validate String Formated in Upper Case

> public Intervention\Validation\Rules\Uppercase::__construct()

The field under validation must be all upper case.

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Uppercase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Uppercase(),
]);
```
