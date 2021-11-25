# Semantic Versioning Rule
## Validate Semantic Version Numbers

> public Intervention\Validation\Rules\SemVer __construct()

The field under validation must be a valid version numbers using [Semantic Versioning](https://semver.org/).

## Parameters

none

## Example

```php
use Intervention\Validation\Rules\SemVer;

$validator = Validator::make($request->all(), [
    'my-value' => new SemVer(),
]);
```