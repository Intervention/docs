---
title: "Snake Case Rule"
subtitle: "Validate String Formated in Snake Case"
---

> public Intervention\Validation\Rules\Snakecase::__construct()

The field under validation must formated as [Snake case](https://en.wikipedia.org/wiki/Snake_case) text.

### Parameters

none

### Example

```php
use Intervention\Validation\Rules\Snakecase;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Snakecase(),
]);
```
