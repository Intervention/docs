# BIC Rule
## Validate a Business Identifier Code
Learn how to validate Business Identifier codes with the additional validation rules of Intervention Validation for your Laravel application.

> public Intervention\Validation\Rules\Bic::__construct()

Checks if field under validation is a valid [Business Identifier Code](https://en.wikipedia.org/wiki/ISO_9362) (BIC).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Bic;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Bic(),
]);
```
