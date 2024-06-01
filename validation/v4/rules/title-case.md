# Title Case Rule
## Validate String Formated in Title Case

> public Intervention\Validation\Rules\Titlecase::__construct()

The field under validation must formated in [Title case](https://en.wikipedia.org/wiki/Title_case).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Titlecase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Titlecase(),
]);
```
