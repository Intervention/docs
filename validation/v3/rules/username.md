# Username Rule
## Validate a typical username

> public Intervention\Validation\Rules\Username::__construct()

The field under validation must be a valid username. Consisting of alpha-numeric characters, underscores, minus and starting with a alphabetic character. Multiple underscore and minus chars are not allowed. Underscore and minus chars are not allowed at the beginning or end.

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Username;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Username(),
]);
```