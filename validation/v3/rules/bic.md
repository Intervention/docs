---
title: "BIC Rule"
subtitle: "Validate a Business Identifier Code"
sort: 1
---

> public Intervention\Validation\Rules\Bic::__construct()

Checks if field under validation is a valid [Business Identifier Code](https://en.wikipedia.org/wiki/ISO_9362) (BIC).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Bic;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Bic(),
]);
```
