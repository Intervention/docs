---
title: "ISBN Rule"
subtitle: "Validate International Standard Book Number"
lead: "Learn how to validate International Static Book Numbers (ISBN) with the additional validation rules of Intervention Validation for your Laravel application."
---

> public Intervention\Validation\Rules\Isbn::__construct(array $lengths = [10, 13])

The field under validation must be a valid [International Standard Book Number](https://en.wikipedia.org/wiki/International_Standard_Book_Number) (ISBN).

### Parameters

#### lengths (optional)

Optional array of allowed lengths to check only for ISBN-10 or ISBN-13.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Isbn;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Isbn(),
]);
```

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Isbn;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Isbn([13]),
]);
```
