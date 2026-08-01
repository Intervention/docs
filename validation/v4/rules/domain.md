---
title: "Domain Name Rule"
subtitle: "Validate Domain Names"
lead: "Validate domain names in Laravel with Intervention Validation. DNS and domain format checks."
sort: 10
---

> public Intervention\Validation\Rules\Domainname::__construct()

The field under validation must be a well-formed [domain name](https://en.wikipedia.org/wiki/Domain_name).

### Parameters

none

### Example

```php
use Illuminate\Support\Facades\Validator;
use Intervention\Validation\Rules\Domainname;

$validator = Validator::make($request->all(), [
    'attribute-key' => new Domainname(),
]);
```
