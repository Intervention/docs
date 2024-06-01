# EAN Rule
## Validate European Article Numbers

> public Intervention\Validation\Rules\Ean::__construct(array $lengths = [8, 13])

Checks for a valid [European Article Number](https://en.wikipedia.org/wiki/International_Article_Number).

### Parameters

#### lengths (optional)

Optional array of allowed lengths (8 or 13) to check only for EAN-8 or EAN-13 or both.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Ean;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Ean(),
]);
```

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Ean;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Ean([8]),
]);
```
