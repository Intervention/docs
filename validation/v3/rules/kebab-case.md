# Kebab Case Rule
## Validate a string in kebab case

> public Intervention\Validation\Rules\Kebabcase __construct()

The value under validation must be formated in [Kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\Kebabcase;

$validator = Validator::make($request->all(), [
    'my-value' => new Kebabcase(),
]);
```


