# HTML Clean Rule
## Validate if text is free of any HTML tags

> public Intervention\Validation\Rules\HtmlClean::__construct()

The field under validation must be free of any html code.

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\HtmlClean;

$validator = Validator::make($request->all(), [
    'attribute-key' => new HtmlClean(),
]);
```


