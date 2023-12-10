# Semantic Versioning Rule
## Validate semantic version numbers

> public Intervention\Validation\Rules\SemVer::__construct()

The field under validation must be a valid version numbers using [Semantic Versioning](https://semver.org/).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\SemVer;

$validator = Validator::make($request->all(), [
    'attribute-key' => new SemVer(),
]);
```