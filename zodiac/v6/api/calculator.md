---
title: "Calculator"
subtitle: "Using the Zodiac Calculator Class"
lead: "Learn how to use the Zodiac Calculator Class to transform different date formats into zodiac sign objects including reading from scalar date types or date objects."
sort: 0
---

[TOC]

## Instantiation

### Constructor

> public Calculator::__construct(Calendar $calendar = Calendar::WESTERN): void

Create the calculator using the constructor. It is possible to specify the
calculation type, which outputs Western zodiac signs by default. 

The calculation method defined here serves as the default; it can be overridden
in the following calculation calls, as you will see later.

#### Parameters

| Name | Type | Description |
| - | - | - |
| calendar | Calendar | Optional calculation method on which the calculation is based. Western by default. |

#### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Calendar;

// create calculator (western by default)
$calculator = new Calculator();

// create calculator for chinese signs
$calculator = new Calculator(Calendar::CHINESE);
```

### Static Factory Method

> public Calculator::withCalendar(Calendar $calendar): CalculatorInterface

Create the calculator using the static factory method. You can specify the
calculation type, which defines the calculation method for all following calls
but can be overridden in the following calculation calls, as you will see
later.

#### Parameters

| Name | Type | Description |
| - | - | - |
| calendar | Calendar | Calculation method on which the calculation is based |

#### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Calendar;

// create calculator for chinese signs
$calculator = Calculator::withCalendar(Calendar::CHINESE);
```

## Calculation

The calculator class can read dates from **integer types** (unix timestamp) as
well as **text strings**, which can represent a relative time, an absolute time
or an unix timestamp as string. It is also possible to read from date objects.

### From String Dates

> public Calculator::fromString(string|Stringable $date, null|Calendar $calendar = null): SignInterface

Create zodiac signs based on the given strings, which can represent a relative
date (`last monday`, `tomorrow` or `last day of next month`) or an absolute
time like `2011-11-16`, `first day of june 2015`.

#### Parameters

| Name | Type | Description |
| - | - | - |
| date | string or Stringable | String representation of a date |
| calendar | null or Calendar | Optional calendar enum value on which the calculation is based (by default either calculator's calendar or western)  |

#### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Calendar;

// create from iso date
$sign = Calculator::fromString('1992-03-19');

// create from relative date
$sign = Calculator::fromString('first day of June 2008');

// calculate chinese zodiac sign from relative date by overriding the default
$sign = Calculator::fromString('first day of June 2008', Calendar::CHINESE);
```

### From Date Objects

> public Calculator::fromDate(DateTimeInterface $date, null|Calendar $calendar = null): SignInterface

Pass date objects (`DateTime` or `Carbon\Carbon`) to instantiate new zodiac objects.

#### Parameters

| Name | Type | Description |
| - | - | - |
| date | DateTimeInterface | Date object to calculate the zodiac sing from |
| calendar | null or Calendar | Optional calendar enum value on which the calculation is based (by default either calculator's calendar or western)  |

#### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Calendar;
use DateTime;
use Carbon\Carbon;

// create western calculator
$calculator = Calculator::withCalendar(Calendar::WESTERN);

// create sign from datetime object
$sign = $calculator->fromDate(new DateTime('1977-03-15'));

// create chinese sign from datetime object
$sign = $calculator->fromDate(new DateTime('1977-03-15'), Calendar::CHINESE);

// create western zodiac sign from carbon object
$zodiac = $calculator->fromDate(Carbon::yesterday());
```

### From Unix Timestamps

> public Calculator::fromUnix(int|string $date, null|Calendar $calendar = null): SignInterface

Calculate zodiac from given unix timestamp date, which can be either an integer or a numeric string.

#### Parameters

| Name | Type | Description |
| - | - | - |
| date | int|string | Unix timestamp date to calculate the zodiac sing from |
| calendar | null or Calendar | Optional calendar enum value on which the calculation is based (by default either calculator's calendar or western)  |

#### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Calendar;

// create calculator (western by default)
$calculator = new Calculator();

// create sign from unix timestamp integer
$sign = $calculator->fromUnix(228268800);

// create sign from unix timestamp string
$sign = $calculator->fromUnix('228268800');

// create chinese zodiac sign from unix timestamp
$sign = $calculator->fromUnix(209262190, Calendar::CHINESE);
```

## Compatibility

### Compare Zodiac Signs

> public Calculator::compare(SignInterface $sign, SignInterface $with): float

It is said that zodiac signs have a certain type of relationship with each
other. While some combinations are said to be compatible, others tend to cause
problems (if you believe in it).

Intervention Zodiac lets you explore this astrological compatibility by
comparing two signs with each other and calculating a compatibility which
ranges from `0` (bad) to `1` (very good).

#### Parameters

| Name | Type | Description |
| - | - | - |
| sign | SignInterface | Sign for comparision |
| with | SignInterface | Zodiac sign to compare with first sign |

#### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Calendar;

// create calculator
$calculator = new Calculator();

// calculate two different birthdays
$joe = $calculator->fromString('1994-08-03');
$jane = $calculator->fromString('1997-03-01');

// calculate compatibility
$compatibility = $calculator->compare($joe, $jane); // .3
```

Continue reading to learn what you can do with the [zodiac objects](/v6/api/sign).
