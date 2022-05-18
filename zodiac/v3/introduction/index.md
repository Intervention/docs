# Intervention Zodiac
## PHP Zodiac Sign Calculator

Intervention Zodiac is a calculator for zodiac signs to resolve the respective zodiac sign from various data types.

### Code Example

```php
use Intervention\Zodiac\Calculator;
use DateTime;
use Carbon\Carbon;

// get zodiac object from a date
$zodiac = Calculator::make('1980-09-15'); // virgo

// method takes mixed formats
$zodiac = Calculator::make('first day of June 2008'); // gemini

// even DateTime objects
$zodiac = Calculator::make(new DateTime('1977-03-15')); // pisces

// get zodiac from a Carbon
$zodiac = Calculator::make(Carbon::yesterday());
```

Read how to [install the package](/v3/introduction/installation).
