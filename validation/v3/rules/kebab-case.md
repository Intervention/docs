---
title: "Kebab Case Rule"
subtitle: "Validate a String in Kebab Case"
sort: 17
---

> public Intervention\Validation\Rules\Kebabcase::__construct()

The value under validation must be formated in [Kebab case](https://en.wikipedia.org/wiki/Letter_case#Special_case_styles).

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Kebabcase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Kebabcase(),
]);
```


