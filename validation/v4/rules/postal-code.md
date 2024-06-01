# Postal Code Rule
## Validate Postal Codes for Individual Countries

> public Intervention\Validation\Rules\Postalcode::__construct(array $countrycodes = [])

The field under validation must be a [postal code](https://en.wikipedia.org/wiki/Postal_code) of the given country.

### Parameters

#### countrycodes

Array of allowed country code strings in [ISO-639-1](https://en.wikipedia.org/wiki/ISO_639-1) format.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Postalcode;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Postalcode(['de', 'nl']),
]);
```

### Validate by Reference

> public Intervention\Validation\Rules\Postalcode::reference(string $reference)

The field under validation must be a [postal code](https://en.wikipedia.org/wiki/Postal_code) 
of the given country. The value to be validated is obtained from the sent data via a reference. 
This can be useful if, for example, you select a country elsewhere and this selection is used 
to determine how the zip code is validated.

### Parameters

#### reference

The key where the country code is stored in the validation data.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Postalcode;

$validator = Validator::make($request->all(), [
    'attribute-key' => Postalcode::reference('country'),
]);
```
