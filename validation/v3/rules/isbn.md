# ISBN Rule
## Validate International Standard Book Number

> public Intervention\Validation\Rules\Isbn __construct(?int $length = null)

The field under validation must be a valid [International Standard Book Number](https://en.wikipedia.org/wiki/International_Standard_Book_Number) (ISBN).

## Parameters

### length (optional)

Optional length parameter as integer to check only for ISBN-10 or ISBN-13.

## Example

```php
use Intervention\Validation\Rules\Isbn;

$validator = Validator::make($request->all(), [
    'my-value' => new Isbn(10),
]);
```


