---
title: "Usage"
subtitle: "How to Use Intervention Zodiac"
lead: "Explore Intervention Zodiac's basic usage, static methods, Laravel integration, and Eloquent Model traits for seamless zodiac attribute generation including code examples for quick implementation."
sort: 2
---

[TOC]

## Basic Usage

Use the [calculator](/v5/api/calculator) class to calculate [zodiac
signs](/v5/api/zodiac) from various date types. The method `zodiac()` acts
as a central starting point. Read the documentation on the [calculator
class](/v5/api/calculator) for more information. 

### Example

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Zodiacs\Scorpio;

$calculator = new Calculator();
$sign = $calculator->zodiac('2000-10-27');

if ($sign instanceof Scorpio) {
    // zodiac sign is scorpio ...
}
```

### Static Example

It's also possible to start the calculation with a static call. See the
following example.

```php
use Intervention\Zodiac\Calculator;

$sign = Calculator::zodiac('2000-10-27');
```

## Usage with Laravel Framework

The package comes with an integrated bridge to the Laravel Framework and
includes a service provider and facade. After the installation Laravel will
automatically register the service provider.

### Example

In Laravel, the `make()` method is used. However, the base class is
different since we are now working with the facade. The service providers
injects the framework's translator automatically. See the following example on
how to calculate a zodiac sign from a get parameter and you can start right
away.

```php
use Illuminate\Support\Facades\Route;
use Illuminate\Http\Request;
use Intervention\Zodiac\Laravel\ZodiacFacade;

Route::get('/', function (Request $request) {
    $sign = ZodiacFacade::make($request->input('birthday'));
    return $sign->localized();
});
```

In Laravel the `localized()` method returns by default in the currently
configured locale.

### Eloquent Model Trait

By including `Intervention\Zodiac\Laravel\Traits\CanResolveZodiac` your
Eloquent Model gets a new zodiac attribute, which is created based on the
birthday attribute of the current model and returns a zodiac object.

#### Include Trait

```php
class User extends Model
{
    // include trait
    use \Intervention\Zodiac\Laravel\Traits\CanResolveZodiac;
    
    // optional: If you want overwrite attribute. By default `birthday`
    protected string $birthdayAttribute = 'date_of_birth';
}
```

#### Zodiac Attribute

```php
// retrieve zodiac attribute
$user = App\User::create(['birthday' => '1980-03-15']);
$zodiac = $user->zodiac; // Intervention\Zodiac\Zodiacs\Pisces
```
