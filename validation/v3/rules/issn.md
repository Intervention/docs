# ISSN Rule
## Validate International Standard Serial Number

> public Intervention\Validation\Rules\Issn::__construct()

Checks for a valid [International Standard Serial Number](https://en.wikipedia.org/wiki/International_Standard_Serial_Number) (ISSN).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\Issn;

$validator = Validator::make($request->all(), [
    'my-value' => new Issn(),
]);
```


