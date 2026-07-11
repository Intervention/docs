---
title: "Language Tag"
subtitle: "Validate IETF BCP 47 language tags"
lead: "Learn how to validate BCP 47 IETF language tags with the additional validation rules of Intervention Validation for your Laravel application."
sort: 25
---

> public Intervention\Validation\Rules\LanguageTag::__construct(string $delimiter = '-', bool $allowScript = false, bool $allowRegion = true, bool $allowVariants = false, bool $allowExtensions = false, bool $allowPrivateUse = false, bool $strict = true)

The field under validation must be a valid [IETF language tag](https://en.wikipedia.org/wiki/ISO_639-1) according to BCP 47 standard.

### Parameters

**delimiter**

Define the delimiter used for validation. Default `-`.

**allowScript**

Specify whether the script subtag is allowed during validation. Default `false.`

**allowRegion**

Specify whether the region subtag is allowed during validation. Default `true.`

**allowVariants**

Specify whether variant subtags are allowed during validation. Default `false.`

**allowExtensions**

Specify whether extension subtags are allowed during validation. Default `false.`

**allowPrivateUse**

Specify whether private use subtags are allowed during validation. Default `false.`

**strict**

If `strict` is `true`, the subtags must be in the correct case. Otherwise, the case doesn't matter. Default `true`.

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\LanguageTag;

$validator = Validator::make($request->all(), [
    'attribute-key' => new LanguageTag(),
]);
```
