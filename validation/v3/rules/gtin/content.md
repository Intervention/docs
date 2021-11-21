> public Intervention\Validation\Rules\Gtin __construct(?int $length = null)

Checks for a valid [Global Trade Item Number](https://en.wikipedia.org/wiki/Global_Trade_Item_Number).

## Parameters

### length (optional)

Optional integer length to check only for certain types (GTIN-8, GTIN-12, GTIN-13 or GTIN-14).

## Example

```php
use Intervention\Validation\Rules\Gtin;

$validator = Validator::make($request->all(), [
    'my-value' => new Gtin(14),
]);
```


