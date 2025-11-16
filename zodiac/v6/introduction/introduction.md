---
title: "Intervention Zodiac"
label: "Introduction"
subtitle: "PHP Zodiac Sign Calculator"
lead: "Intervention Zodiac is a calculator for zodiac signs to resolve the respective star sign from various data types."
sort: 0
---

### Code Examples

```php
use Intervention\Zodiac\Calculator;
use DateTime;
use Carbon\Carbon;

// get zodiac object from a date
$sign = Calculator::fromString('1980-09-15');

// method takes mixed string formats
$sign = Calculator::fromString('first day of June 2008');

// Create zodiac sign from DateTime objects
$sign = Calculator::fromDate(new DateTime('1977-03-15'));

// since Carbon dates extend from DateTime they can also be read
$sign = Calculator::fromDate(Carbon::yesterday());

// or use the dedicated method to create from carbon dates
$sign = Calculator::fromCarbon(Carbon::yesterday());

// get zodiac from unix timestamp
$sign = Calculator::fromUnix(228268800);
```

```php
use Intervention\Zodiac\Calculator;
use DateTime;
use Carbon\Carbon;

// calculate zodiac sign
$sign = Calculator::fromString('1977-06-17');

$name = $zodiac->name(); // 'gemini'
$html = $zodiac->html(); // '♊︎'
$localized = $zodiac->localized('fr'); // Gémeaux
$compatibility = $zodiac->compatibility($zodiac); // 6
```

Read how to [install the package](/v6/introduction/installation).
