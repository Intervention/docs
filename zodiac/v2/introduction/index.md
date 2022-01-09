# Intervention Zodiac
## PHP Zodiac Sign Calculator

Intervention Zodiac is a calculator for zodiac signs to resolve the respective zodiac sign from various data types.

### Code Example

```php
use Intervention\Zodiac\Calculator;

// get zodiac object from a date
$zodiac = Zodiac::make('1980-09-15'); // virgo

// method takes mixed formats
$zodiac = Zodiac::make('first day of June 2008'); // gemini

// even DateTime objects
$zodiac = Zodiac::make(new DateTime('1977-03-15')); // pisces

// get zodiac from a Carbon
$zodiac = Zodiac::make(Carbon::yesterday());
```

Read how to [install the package](/v2/introduction/installation).