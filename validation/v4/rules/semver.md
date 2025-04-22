---
title: "Semantic Versioning Rule"
subtitle: "Validate Semantic Version Numbers"
lead: "Learn how to validate Semantic Version Numbers (semver) with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\SemVer::__construct()

The field under validation must be a valid version numbers using [Semantic Versioning](https://semver.org/).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\SemVer;

$validator = Validator::make($request->all(), [
    'attribute-key' => new SemVer(),
]);
```
