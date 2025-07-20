---
title: "EAN Rule"
subtitle: "Validate European Article Numbers"
sort: 7
---

> public Intervention\Validation\Rules\Ean::__construct(?int $length = null)

Checks for a valid [European Article Number](https://en.wikipedia.org/wiki/International_Article_Number).

### Parameters

#### length (optional)

Optional integer length (8 or 13) to check only for EAN-8 or EAN-13 or either one if not present.

### Example

```php
use Intervention\Validation\Rules\Ean;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Ean(8),
]);
```


