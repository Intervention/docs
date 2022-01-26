# MAC address Rule
## Validate a MAC address

> public Intervention\Validation\Rules\MacAddress::__construct()

The field under validation must be a [media access control address](https://en.wikipedia.org/wiki/MAC_address) (MAC address).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\MacAddress;

$validator = Validator::make($request->all(), [
    'attribute-key' => new MacAddress(),
]);
```


