# Austrian Social Insurance Number Rule
## Validate the Austria Social Insurance Number

> public Intervention\Validation\Rules\AustrianInsuranceNumber::__construct()

Checks for a valid [austrian social insurance number](https://www.sozialversicherung.at/cdscontent/?contentid=10007.820902&viewmode=content).

### Example

```php
use Intervention\Validation\Rules\AustrianInsuranceNumber;

// validate GTIN
$validator = Validator::make($request->all(), [
    'attribute-key' => new AustrianInsuranceNumber(),
]);
```
