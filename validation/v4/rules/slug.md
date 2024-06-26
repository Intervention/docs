# Slug Rule
## Validate a SEO-friendly Short Text

> public Intervention\Validation\Rules\Slug::__construct()

The field under validation must be a user- and [SEO-friendly short text](https://en.wikipedia.org/wiki/Clean_URL#Slug).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Slug;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Slug(),
]);
```
