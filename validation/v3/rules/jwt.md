# JWT Rule
## Validate a JSON Web Token

> public Intervention\Validation\Rules\Jwt::__construct()

The value under validation must be a in format of a [JSON Web Token](https://en.wikipedia.org/wiki/JSON_Web_Token).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\Jwt;

$validator = Validator::make($request->all(), [
    'my-value' => new Jwt(),
]);
```


