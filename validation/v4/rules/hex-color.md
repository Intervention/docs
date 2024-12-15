# Hexadecimal Color Rule
## Validate a Hexadecimal Color Code
Explore how to validate hexadecimal color colors also known as web colors with the additional validation rules of Intervention Validation for your Laravel application.

> public Intervention\Validation\Rules\HexColor::__construct(array $lengths = [3, 4, 6, 8])

The field under validation must be a valid [hexadecimal color code](https://en.wikipedia.org/wiki/Web_colors). 

### Parameters

#### lengths (optional)

Pass optionally allowed lengths as an array to check only for shorthand (3 or 4 characters) or full hexadecimal (6 or 8 characters) form or combinations.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\HexColor;

$validator = Validator::make($request->all(), [
    'attribute-key' => new HexColor([3, 6]),
]);
```
