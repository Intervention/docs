---
title: "Intervention Zodiac"
label: "Introduction"
subtitle: "PHP Zodiac Sign Calculator"
lead: "Intervention Zodiac is a calculator for zodiac signs to resolve the respective star sign from various data types."
sort: 0
---

## Zodiac Calculator

Intervention Zodiac is a powerful, developer-friendly tool for effortless
zodiac sign calculation. This versatile PHP library lets you generate zodiac
signs from nearly any date format, including natural language strings, Unix
timestamps, standard `DateTime` objects, and Carbon instances. 

Whether you're building horoscope features or astrology apps the Zodiac
Calculator effortless delivers results for western as well as traditional
chinese zodiac signs.

### Code Examples

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Calendar;
use DateTime;

// get zodiac object from a date
$sign = Calculator::fromString('1980-09-15');

// create zodiac sign from DateTime objects
$sign = Calculator::fromDate(new DateTime('1977-03-15'));

// create zodiac sign from DateTime objects
$sign = Calculator::fromDate(new DateTime('1977-03-15'));

// calculate chinese zodiac signs
$sign = Calculator::fromString('1977-06-17', Calendar::CHINESE);
```

Read more about the [calculator](/v6/api/calculator).

## Zodiac Signs

Unlock insights by accessing the countless data properties of zodiac sign
objects. Designed for flexible data handling, the sign instances come with
built-in language translation and even compatibility scores.

### Code Examples

```php
use Intervention\Zodiac\Calculator;
use DateTime;
use Carbon\Carbon;

// calculate zodiac sign
$sign = Calculator::fromString('1977-06-17');

$name = $sign->name(); // 'gemini'
$html = $sign->html(); // '♊︎'
$localized = $sign->localized('fr'); // 'Gémeaux'
$compatibility = $sign->compatibility($sign); // 6
```

Read more about [zodiac signs](/v6/api/sign) or how to [install the package](/v6/introduction/installation).
