# Domain Name Rule
## Validate Domain Names

> public Intervention\Validation\Rules\Domainname::__construct()

The field under validation must be a well formed [domainname](https://en.wikipedia.org/wiki/Domain_name).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Domainname;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Domainname(),
]);
```
