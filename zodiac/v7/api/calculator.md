---
title: "Calculator"
subtitle: "Using the Zodiac Calculator Class"
lead: "Learn how to use the Zodiac Calculator Class to transform different date formats into zodiac sign objects including reading from scalar date types or date objects."
sort: 0
---

[TOC]

## Instantiation

### Constructor

> public Calculator::__construct(Astrology $astrology = Astrology::WESTERN): void

Create the calculator using the constructor. It is possible to specify the
astrology, which outputs Western zodiac signs by default. 

The astrology defined here serves as the default; it can be overridden
in the calculation calls, as you will see later.

#### Parameters

| Name | Type | Description |
| - | - | - |
| astrology | Astrology | Optional astrology on which the calculation is based. Western by default. |

#### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Astrology;

// create calculator (western by default)
$calculator = new Calculator();

// create calculator for chinese signs only
$calculator = new Calculator(Astrology::CHINESE);
```

### Static Factory Method

> public Calculator::create(Astrology $astrology = Astrology::WESTERN): CalculatorInterface

Create the calculator using the static factory method. You can specify the
astrology type, which defines the calculation method for all following calls
but can be overridden in the following calculation calls, as you will see
later.

#### Parameters

| Name | Type | Description |
| - | - | - |
| astrology | Astrology | Astrology type on which the calculation is based |

#### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Astrology;

// create calculator (western by default)
$calculator = Calculator::create();

// create calculator for chinese signs
$calculator = Calculator::create(Astrology::CHINESE);
```

### Factory Method for Western Calculator

> public Calculator::western(): CalculatorInterface

Create a calculator using the static factory method for western astrology directly.

#### Example

```php
use Intervention\Zodiac\Calculator;

// create calculator for western signs
$calculator = Calculator::western();
```

### Factory Method for Chinese Calculator

> public Calculator::chinese(): CalculatorInterface

Create a calculator using the static factory method for chinese astrology directly.

**Please note that calculations for Chinese zodiac signs are currently only implemented for years between 1900 and 2100.**

#### Example

```php
use Intervention\Zodiac\Calculator;

// create calculator for chinese signs
$calculator = Calculator::chinese();
```

## Calculation

The calculator class can read dates from **integer types** (unix timestamp) as
well as **text strings**, which can represent a relative time, an absolute time
or an unix timestamp as string. It is also possible to read from date objects.

### Calculate various date types

> public Calculator::calculate(string|Stringable|int|float|DateTimeInterface $date, ?Astrology $astrology = null): SignInterface

Calculate zodiac signs from the a date, which can be given in various formats.

#### Parameters

| Name | Type | Description |
| - | - | - |
| date | string, Stringable, int, float, DateTimeInterface | The date for which the zodiac sign is to be calculated |
| astrology | null or Astrology | Optional astrology enum value on which the calculation is based. By default the calculator's astrology will be used. |

#### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Astrology;
use DateTime;
use Carbon\Carbon;

// create calculator
$calculator = new Calculator(Astrology::WESTERN);

// create from iso date
$sign = Calculator::calculate('1992-03-19');

// create from relative date
$sign = Calculator::calculate('first day of June 2008');

// calculate chinese zodiac sign from relative date by overriding the default
$sign = Calculator::calculate('first day of June 2008', Astrology::CHINESE);

// create sign from datetime object
$sign = $calculator->calculate(new DateTime('1977-03-15'));

// create chinese sign from datetime object
$sign = $calculator->calculate(new DateTime('1977-03-15'), Astrology::CHINESE);

// create western zodiac sign from carbon object
$zodiac = $calculator->calculate(Carbon::yesterday());

// create sign from unix timestamp integer
$sign = $calculator->calculate(228268800);

// create sign from unix timestamp string
$sign = $calculator->calculate('228268800');

// create chinese zodiac sign from unix timestamp
$sign = $calculator->calculate(209262190, Astrology::CHINESE);

```

Continue reading to learn what you can do with the [zodiac objects](/v7/api/sign).
