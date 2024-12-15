# Slug Rule
## Validate a SEO-friendly Short Text
Explore how to validate SEO-friendly short texts with the additional validation rules of Intervention Validation for your Laravel application.

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
