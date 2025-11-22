---
title: "Zodiac Sign"
subtitle: "Working with Zodiac Sign Objects"
lead: "Discover how to use the zodiac objects returned by the Intervention Image Zodiac Calculator. Generate localized contents and use a compatibility calculator based on astrological theory."
sort: 1
---

[TOC]

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

### Localized Title

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
