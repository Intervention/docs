---
title: "Intervention Zodiac"
label: "Introduction"
subtitle: "PHP Zodiac Sign Calculator"
lead: "Intervention Zodiac is a astrological calculator that resolves Western and Chinese zodiac signs from various data types."
sort: 0
---

## Zodiac Calculator

Intervention Zodiac is a powerful, developer-friendly tool for effortless
zodiac sign calculation. This versatile PHP library lets you generate zodiac
signs from various date formats, including natural language strings, Unix
timestamps, standard `DateTime` objects, and Carbon instances. 

Whether you're building horoscope features or astrology apps the Zodiac
Calculator effortless delivers results for western as well as traditional
chinese zodiac signs.

- Fluent interface to calculate zodiac signs
- Support for western and chinese astrology
- Framework-agnostic

### Code Examples

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Astrology;
use Carbon\Carbon;
use DateTime;

// create calculator
$calculator = new Calculator(Astrology::WESTERN);

// calculate various date formats
$sign = $calculator->calculate('2001-01-01');
$sign = $calculator->calculate('first day of june 2014');
$sign = $calculator->calculate('2018-06-15 12:34:00');
$sign = $calculator->calculate(new DateTime('2001-01-01'));
$sign = $calculator->calculate(Carbon::yesterday());
$sign = $calculator->calculate(228268800);
$sign = $calculator->calculate('228268800');

// override the default astrology
$sign = $calculator->calculate('2001-01-01', Astrology::CHINESE);
```

Read more about the [calculator](/v7/api/calculator).

## Zodiac Signs

Unlock insights by accessing the countless data properties of zodiac sign
objects. Designed for flexible data handling, the sign instances come with
built-in language translation and even compatibility scores.

### Code Examples

```php
use Intervention\Zodiac\Sign;
use Intervention\Zodiac\Chinese\Sign as ChineseSign;
use Intervention\Zodiac\Western\Sign as WesternSign;
use DateTime;
use Carbon\Carbon;

// parse signs directly
$sign = Sign::fromString('2000-01-01');
$sign = Sign::fromString('first day of june 2014', Astrology::CHINESE);
$sign = Sign::fromDate(new DateTime('2001-01-01'), Astrology::WESTERN);
$sign = Sign::fromCarbon(Carbon::yesterday(), Astrology::CHINESE);
$sign = Sign::fromUnix(228268800, Astrology::WESTERN);
$sign = Sign::fromUnix('228268800', Astrology::CHINESE);

// parse only western signs
$sign = WesternSign::fromString('2000-01-01');

// parse only chinese signs
$sign = ChineseSign::fromString('2000-01-01');

// sign methods
$name = $sign->name(); // 'gemini'
$html = $sign->html(); // '♊︎'
$localized = $sign->localize('fr')->name(); // Gémeaux
$compatibility = $sign->compatibility($sign); // .6
```

Read more about [zodiac signs](/v7/api/sign) or how to [install the package](/v7/introduction/installation).
