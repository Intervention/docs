> public Intervention\Validation\Rules\Cidr __construct()

Check if the field under validation is a [Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) notation (CIDR).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\Cidr;

$validator = Validator::make($request->all(), [
    'my-value' => new Cidr(),
]);
```
