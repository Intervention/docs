# Zodiac
## Working with Zodiac Objects

[TOC]

The zodiac objects returned from the [calculator](/v4/api/calculator) can be
used in the following ways.

### Zodiac Name

> public Zodiac::name(): string

Return the name of the current zodiac. This is more a identification key than a
textual title. It's possible to cast the zodiac object to a string type to get
the same result.

```php
use Intervention\Zodiac\Calculator;

// create from iso date
$zodiac = Calculator::make('1977-06-17');
$name = $zodiac->name(); // "gemini"
$name = (string) $zodiac; // "gemini"
```

### Localized Title

> public Zodiac::localized(?string $locale = null): string

Return the localized title of the current zodiac in the given locale. The
locale parameter is optional, by default the english language is returned.

```php
use Intervention\Zodiac\Calculator;

// create from iso date
$zodiac = Calculator::make('1977-06-17');
$name = $zodiac->localized('fr'); // Gémeaux
```

### HTML Representation

> public Zodiac::html(): string

Returns the [HTML UTF-8 symbol
code](https://www.w3schools.com/charsets/ref_utf_symbols.asp) representing an
icon of the current zodiac sign.

```php
use Intervention\Zodiac\Calculator;

// create from iso date
$zodiac = Calculator::make('1977-06-17');
$name = $zodiac->html(); // &#9802;
```

### Zodiac Sign Compatibility

> public Zodiac::compatibility(ZodiacInterface $zodiac): float

This method calculates how a person with the current star sign matches another
person with the given sign according to astrological theory.

The factor is returned as a float value of `0-1`, with a higher value
representing more compatibility.

This value is completely made up, so don't plan your life decisions around it.


```php
use Intervention\Zodiac\Calculator;

$gemini = Calculator::make('1997-06-17'); // Intervention\Zodiac\Zodiacs\Gemini
$virgo = Calculator::make('2000-09-10'); // Intervention\Zodiac\Zodiacs\Virgo

$factor = $gemini->compatibility($virgo);
```
