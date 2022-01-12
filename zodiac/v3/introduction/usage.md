# Usage
## How to Use Intervention Zodiac

[TOC]

## Basic Usage

Use the [calculator](/v3/api/calculator) class to calculate zodiac signs from various date types. The method `make` reads different date types. Reed the documentation on the [calculator class](/v2/api/calculator) for more information. 

### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Zodiacs\Scorpio;

$calculator = new Calculator();
$sign = $calculator->make('2000-10-27');

if ($zodiac instanceof Scorpio) {
    // my zodiac sign is scorpio ...
}
```

### Static Example

It's also possible to start the calculate with a static call. See the following example.

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Zodiacs\Scorpio;

$sign = Calculator::make('2000-10-27');
```

## Usage with Laravel Framework

The package comes with integrated bridge to the Laravel Framework and includes a service provider and facades. After the installation Laravel will automatically register the service provider.

### Example

In Laravel, the `make()` method is also used. However, the base class is different since we are now working with the facade. The service providers injects the framework's translator automatically. See the following example on how to calculate a zodiac sign from a get parameter.

```php
use Illuminate\Support\Facades\Route;
use Illuminate\Http\Request;

Route::get('/', function (Request $request) {
    $sign = Zodiac::make($request->input('birthday'));
    return $sign->localized();
});
```