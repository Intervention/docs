# Intervention Zodiac
## PHP Zodiac Sign Calculator

Intervention Zodiac is a calculator for zodiac signs to resolve the respective
star sign from various data types.

### Code Examples

```php
use Intervention\Zodiac\Calculator;
use DateTime;
use Carbon\Carbon;

// calculate zodiac sign from a string date
$zodiac = Calculator::zodiac('1980-09-15'); // virgo

// calculate zodiac sign from a string date
$zodiac = Calculator::zodiac('first day of June 2008'); // gemini

// calculate zodiac sign from DateTime object
$zodiac = Calculator::zodiac(new DateTime('1977-03-15')); // pisces

// get zodiac from a Carbon object
$zodiac = Calculator::zodiac(Carbon::yesterday());

// get zodiac from a Carbon object
$zodiac = Calculator::zodiac(228268800);
```

```php
use Intervention\Zodiac\Calculator;
use DateTime;
use Carbon\Carbon;

// calculate zodiac sing
$zodiac = Calculator::zodiac('1977-06-17');

$name = $zodiac->name(); // 'gemini'
$html = $zodiac->html(); // '♊︎'
$localized = $zodiac->localized('fr'); // Gémeaux
$compatibility = $zodiac->compatibility($zodiac); // 6
```

Read how to [install the package](/v5/introduction/installation).
