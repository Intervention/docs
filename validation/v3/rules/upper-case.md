---
title: "Upper Case Rule"
subtitle: "Validate String Formated in Upper Case"
sort: 27
---

> public Intervention\Validation\Rules\Uppercase::__construct()

The field under validation must be all upper case.

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Uppercase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Uppercase(),
]);
```
