---
title: "GRid Rule"
subtitle: "Validate Global Release Identifier (GRid)"
lead: "Learn how to validate the Global Release Identifier (GRid) format with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Grid::__construct()

Checks for a valid [Global Release Identifier](https://en.wikipedia.org/wiki/Global_Release_Identifier) (GRid).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Grid;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Grid(),
]);
```

