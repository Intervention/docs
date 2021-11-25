# Lower Case Rule
## Validate a string in lower case

> public Intervention\Validation\Rules\Lowercase __construct()

The given value must be all lower case letters.

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\Lowercase;

$validator = Validator::make($request->all(), [
    'my-value' => new Lowercase(),
]);
```


