# ISBN Rule
## Validate International Standard Book Number

> public Intervention\Validation\Rules\Isbn::__construct(array $lengths = [10, 13])

The field under validation must be a valid [International Standard Book Number](https://en.wikipedia.org/wiki/International_Standard_Book_Number) (ISBN).

### Parameters

#### lengths (optional)

Optional array of allowed lengths to check only for ISBN-10 or ISBN-13.

### Example

```php
use Intervention\Validation\Rules\Isbn;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Isbn(),
]);
```

```php
use Intervention\Validation\Rules\Isbn;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Isbn([13]),
]);
```
