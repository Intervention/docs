---
title: "Slug Rule"
subtitle: "Validate a SEO-friendly Short Text"
sort: 23
---

> public Intervention\Validation\Rules\Slug::__construct()

The field under validation must be a user- and [SEO-friendly short text](https://en.wikipedia.org/wiki/Clean_URL#Slug).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Slug;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Slug(),
]);
```
