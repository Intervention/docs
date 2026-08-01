---
title: "Slug Rule"
subtitle: "Validate a SEO-friendly Short Text"
lead: "Validate SEO-friendly URL slugs in Laravel with Intervention Validation. Check slug format and structure."
sort: 31
---

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
