# Camel case Rule
## Validate camel case string

> public Intervention\Validation\Rules\Camelcase::__construct()

The field under validation must be a formated in [Camel case](https://en.wikipedia.org/wiki/Camel_case).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Camelcase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Camelcase(),
]);
```
