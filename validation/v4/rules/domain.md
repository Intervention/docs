# Domain Name Rule
## Validate Domain Names
Learn how to validate the domain names with the additional validation rules of Intervention Validation for your Laravel application.

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
