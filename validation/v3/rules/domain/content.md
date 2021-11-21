> public Intervention\Validation\Rules\Domainname __construct()

The field under validation must be a well formed [domainname](https://en.wikipedia.org/wiki/Domain_name).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\Domainname;

$validator = Validator::make($request->all(), [
    'my-value' => new Domainname(),
]);
```
