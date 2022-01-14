# Calculator
## Using the Zodiac Calculator Class

[TOC]

The calculator class works a a starting point to transform different types of dates into zodiac objects.

### Instantiate from Scalar Dates

The calculator class can read dates from **integer types** (unix timestamp) as well as **text strings**, which can represent a relative time (last monday, tomorrow, last day of next month) or an absolute time (first day of June 1983, 2011-11-11).

```php
use Intervention\Zodiac\Calculator;

// create from iso date
$zodiac = Calculator::make('1992-03-19');

// create from relative date
$zodiac = (string) Calculator::make('first day of June 2008');

// create from unix timestamp integer
$zodiac = (string) Calculator::make(1641719287);
```

### Instantiate from Date Objects

You can also pass date objects (`DateTime` or `Carbon`) to instantiate new zodiac objects.

```php
use Intervention\Zodiac\Calculator;

// create from datetime objects
$zodiac = Calculator::make(new DateTime('1977-03-15'));

// create from carbon objects
$zodiac = Calculator::make(Carbon::yesterday());
```

Continue reading to learn what you can do with the [zodiac objects](/v3/api/zodiac).