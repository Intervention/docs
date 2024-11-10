# Calculator
## Using the Zodiac Calculator Class

[TOC]

The calculator class works as a starting point to transform different types of
dates into zodiac objects.

### Instantiate from Scalar Dates

The calculator class can read dates from **integer types** (unix timestamp) as
well as **text strings**, which can represent a relative time (`last monday`,
`tomorrow`, `last day of next month`), an absolute time (`first day of June 1983`,
`2011-11-11`) or an unix timestamp as string.

```php
use Intervention\Zodiac\Calculator;

// create from iso date
$zodiac = Calculator::zodiac('1992-03-19');

// create from relative date
$zodiac = Calculator::zodiac('first day of June 2008');

// create from unix timestamp integer
$zodiac = Calculator::zodiac(1641719287);
```

### Instantiate from Objects

You can also pass date objects (`DateTime` or `Carbon`) to instantiate new zodiac objects.

```php
use Intervention\Zodiac\Calculator;
use Carbon\Carbon;

// create from datetime objects
$zodiac = Calculator::zodiac(new DateTime('1977-03-15'));

// create from carbon objects
$zodiac = Calculator::zodiac(Carbon::yesterday());
```

Continue reading to learn what you can do with the [zodiac objects](/v5/api/zodiac).
