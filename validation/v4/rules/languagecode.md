---
title: "Language Code"
subtitle: "Validate ISO 639-1 Language Codes"
lead: "Validate ISO 639-1 language codes in Laravel with Intervention Validation. Two-letter language identifiers."
sort: 24
---

> public Intervention\Validation\Rules\LanguageCode::__construct(bool $strict = true)

The field under validation must be a valid [language code](https://en.wikipedia.org/wiki/ISO_639-1) according to ISO ISO 639-1.

### Parameters

**strict**

If `strict` is `true`, the language code must be passed in lowercase. Otherwise, the case doesn't matter.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\LanguageCode;

$validator = Validator::make($request->all(), [
    'attribute-key' => new LanguageCode(),
]);
```
