# Hexadecimal Color Rule
## Validate a hexadecimal color code

> public Intervention\Validation\Rules\HexColor __construct(?int $length = null)

The field under validation must be a valid [hexadecimal color code](https://en.wikipedia.org/wiki/Web_colors). 

## Parameters

### length (optional)

Optional length as integer to check only for shorthand (3 characters) or full hexadecimal (6 characters) form.

## Example

```php
use Intervention\Validation\Rules\HexColor;

$validator = Validator::make($request->all(), [
    'my-value' => new HexColor(3),
]);
```


