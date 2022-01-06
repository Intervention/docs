# Calculator
## Using the zodiac calculator class

The calculator class works a a starting point to transform different types of **date data** into zodiac objects.

### Instantiate from text dates

The calculator class can read dates in text format, which can represent a relative time (last monday, tomorrow, last day of next month) or an absolute time (first day of June 1983, 2011-11-11).

```php
use Intervention\Zodiac\Calculator;

// create from iso date
$zodiac = Calculator::make('1980-09-15');

// create from iso date
$zodiac = (string) Calculator::make('first day of June 2008');
```

### Instantiate from date objects

You can also pass date objects (`DateTime` or `Carbon`) to instantiate new zodiac objects.

```php
use Intervention\Zodiac\Calculator;

// create from datetime objects
$zodiac = Calculator::make(new DateTime('1977-03-15'));

// create from carbon objects
$zodiac = Calculator::make(Carbon::yesterday());
```

Continue reading to learn what you can do with the [zodiac objects](/v2/usage/zodiac).