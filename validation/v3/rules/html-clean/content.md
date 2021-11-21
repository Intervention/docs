> public Intervention\Validation\Rules\HtmlClean __construct()

The field under validation must be free of any html code.

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\HtmlClean;

$validator = Validator::make($request->all(), [
    'my-value' => new HtmlClean(),
]);
```


