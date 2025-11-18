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
use Intervention\Zodiac\Astrology;
use Carbon\Carbon;
use DateTime;

$sign = Calculator::fromString('2001-01-01');
$sign = Calculator::fromString('2001-01-01', Astrology::CHINESE);

// create western calculator
$sign = Calculator::western()
    ->fromString('2001-01-01'); 

// create chinese calculator
$sign = Calculator::chinese()
    ->fromString('2001-01-01'); 

// override default
$sign = Calculator::western()
    ->fromString('2001-01-01', Astrology::CHINESE);

// pass astrology as a parameter
$sign = Calculator::withAstrology(Astrology::CHINESE)
    ->fromString('2001-01-01');

// override default
$sign = Calculator::withAstrology(Astrology::CHINESE)
    ->fromString('2001-01-01', Astrology::WESTERN);

// parse various date formats
$sign = Calculator::fromString('first day of june 2014');
$sign = Calculator::fromString('2018-06-15 12:34:00');
$sign = Calculator::fromDate(new DateTime('2001-01-01'));
$sign = Calculator::fromDate(Carbon::yesterday());
$sign = Calculator::fromUnix(228268800);
$sign = Calculator::fromUnix('228268800');
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

// calculate zodiac sing
$sign = Calculator::fromDate($date);

$name = $sign->name(); // 'gemini'
$html = $sign->html(); // '♊︎'
$localized = $sign->localize('fr')->name(); // Gémeaux
$compatibility = $sign->compatibility($sign); // .6
```

Read more about [zodiac signs](/v6/api/sign) or how to [install the package](/v6/introduction/installation).
