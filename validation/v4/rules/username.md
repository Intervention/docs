---
title: "Username Rule"
subtitle: "Validate a Typical Username"
lead: "Explore how to validate typical usernames with the additional validation rules of Intervention Validation for your Laravel application."
sort: 31
---

> public Intervention\Validation\Rules\Username::__construct()

The field under validation must be a valid username consisting of alphanumeric characters, underscores, and hyphens, starting with an alphabetic character. Multiple consecutive underscores and hyphens are not allowed. Underscores and hyphens are not allowed at the beginning or end.

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Username;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Username(),
]);
```
