---
title: "Zodiac Sign"
subtitle: "Working with Zodiac Sign Objects"
lead: "Discover how to use the zodiac objects returned by the Intervention Image Zodiac Calculator. Generate localized contents and use a compatibility calculator based on astrological theory."
sort: 1
---

[TOC]

## Zodiac Factory Methods

### Create Zodiac Signs from String Dates

> public static Sign::fromString(string|Stringable $date, Astrology $astrology = Astrology::WESTERN): SignInterface

Create zodiac signs based on the given strings, which can represent a relative
date (`last monday`, `tomorrow` or `last day of next month`) or an absolute time like
`2011-11-16`, `first day of june 2015`.

#### Example

```php
use Intervention\Zodiac\Sign;
use Intervention\Zodiac\Western\Sign as WesternSign;
use Intervention\Zodiac\Chinese\Sign as ChineseSign;

// parse zodiac sign from string values
$sign = Sign::fromString('2000-01-01');
$sign = Sign::fromString('first day of june 2014', Astrology::CHINESE);

// parse only western signs
$sign = WesternSign::fromString('2000-01-01');

// parse only chinese signs
$sign = ChineseSign::fromString('2000-01-01');
```

### Create Zodiac Signs from Date Objects

> public static Sign::fromDate(DateTimeInterface $date, Astrology $astrology = Astrology::WESTERN): SignInterface

Create zodiac signs from date objects like `DateTime` or `Carbon\Carbon`.

#### Example

```php
use Intervention\Zodiac\Sign;
use Intervention\Zodiac\Western\Sign as WesternSign;
use Intervention\Zodiac\Chinese\Sign as ChineseSign;

// parse zodiac sign from date objects
$sign = Sign::fromDate(new DateTime('1977-03-15'));
$sign = Sign::fromDate(Carbon\Carbon::yesterday(), Astrology::CHINESE);

// parse only western signs
$sign = WesternSign::fromDate(new DateTime('1977-03-15'));

// parse only chinese signs
$sign = ChineseSign::fromDate(new DateTime('1977-03-15'));
```

### Create Zodiac Signs from Carbon objects

> public static Sign::fromCarbon(CarbonInterface $date, Astrology $astrology = Astrology::WESTERN): SignInterface

Pass date carbon date objects like `Carbon\Carbon` to instantiate new zodiac objects.

#### Example

```php
use Intervention\Zodiac\Sign;
use Intervention\Zodiac\Western\Sign as WesternSign;
use Intervention\Zodiac\Chinese\Sign as ChineseSign;

// parse zodiac sign from carbon date
$sign = Sign::fromCarbon(Carbon\Carbon::yesterday(), Astrology::CHINESE);

// parse only western signs
$sign = WesternSign::fromCarbon(Carbon\Carbon::yesterday());

// parse only chinese signs
$sign = ChineseSign::fromCarbon(Carbon\Carbon::yesterday());
```

### Create Zodiac Signs from Unix Timestamps

> public static Sign::fromUnix(int|float|string $date, Astrology $astrology = Astrology::WESTERN): SignInterface

Calculate zodiac from given unix timestamp date, which can be either an integer or a numeric string.

#### Example

```php
use Intervention\Zodiac\Sign;
use Intervention\Zodiac\Western\Sign as WesternSign;
use Intervention\Zodiac\Chinese\Sign as ChineseSign;

// parse zodiac sign from unix timestamps
$sign = Sign::fromUnix(228268800);
$sign = Sign::fromUnix('228268800');

// parse only western signs
$sign = WesternSign::fromUnix(228268800);

// parse only chinese signs
$sign = ChineseSign::fromUnix(228268800);
```

## Zodiac Methods

### Zodiac Name

> public SignInterface::name(): string

Return the english name of the current zodiac sign. It's possible to cast the zodiac
object to a string type to get the same result. If you want an localized name
you can use the `localize()` method first.

#### Example

```php
use Intervention\Zodiac\Calculator;

// create from iso date
$zodiac = Calculator::fromString('1977-06-17');
$name = $zodiac->name(); // "gemini"
$name = (string) $zodiac; // "gemini"
```

### Localization

> public SignInterface::localize(?string $locale = null): SignInterface

Return the localized version of the zodiac sign in the given locale. The
locale parameter is optional, by default the english language is returned.

#### Example

```php
use Intervention\Zodiac\Calculator;

// calculate zodiac sign
$zodiac = Calculator::fromString('1977-06-17');
$name = $zodiac->localize('fr')–>name(); // Gémeaux
```

### HTML Representation

> public SignInterface::html(): string

Returns the [HTML UTF-8 symbol code](https://www.w3schools.com/charsets/ref_utf_symbols.asp) 
representing an icon of the current zodiac sign.

```php
use Intervention\Zodiac\Calculator;

// create zodiac sign from date
$zodiac = Calculator::fromString('1977-06-17');
$name = $zodiac->html(); // &#9802;
```

### Zodiac Sign Compatibility

> public SignInterface::compatibility(ZodiacInterface $sign): float

Some say said that zodiac signs have a certain type astrological compatibility
with each other. While some combinations are said to be compatible, others not
so much (if you believe in it).

This method lets you explore this astrological compatibility by
comparing the current instance to another sign.

The compatibility factor is returned as a float value of `0-1`, with a higher
value representing more compatibility.

#### Example

```php
use Intervention\Zodiac\Calculator;

$gemini = Calculator::fromString('1997-06-17'); // Intervention\Zodiac\Zodiacs\Gemini
$virgo = Calculator::fromString('2000-09-10'); // Intervention\Zodiac\Zodiacs\Virgo

$factor = $gemini->compatibility($virgo);
```
