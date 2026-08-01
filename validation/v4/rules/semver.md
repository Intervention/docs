---
title: "Semantic Versioning Rule"
subtitle: "Validate Semantic Version Numbers"
lead: "Validate Semantic Version Numbers (semver) in Laravel with Intervention Validation. Version format checks."
sort: 30
---

> public Intervention\Validation\Rules\SemVer::__construct()

The field under validation must be a valid version number using [Semantic Versioning](https://semver.org/).

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
