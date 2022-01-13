# Usage
## How to Use Intervention Zodiac

[TOC]

## Basic Usage

Use the [calculator](/v3/api/calculator) class to calculate [zodiac signs](/v3/api/zodiac) from various date types. The method `make` reads different date types. Reed the documentation on the [calculator class](/v2/api/calculator) for more information. 

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

It's also possible to start the calculation with a static call. See the following example.

```php
use Intervention\Zodiac\Calculator;
use Intervention\Zodiac\Zodiacs\Scorpio;

$sign = Calculator::make('2000-10-27');
```

## Usage with Laravel Framework

The package comes with an integrated bridge to the Laravel Framework and includes a service provider and facade. After the installation Laravel will automatically register the service provider.

### Example

In Laravel, the `make()` method is also used. However, the base class is different since we are now working with the facade. The service providers injects the framework's translator automatically. See the following example on how to calculate a zodiac sign from a get parameter and you can start right away.

```php
use Illuminate\Support\Facades\Route;
use Illuminate\Http\Request;

Route::get('/', function (Request $request) {
    $sign = Zodiac::make($request->input('birthday'));
    return $sign->localized();
});
```

In Laravel the `localized()` method returns by default in the currently configured locale.

### Eloquent Model Trait

By including `Intervention\Zodiac\Laravel\Traits\CanResolveZodiac` your Eloquent Model gets a new zodiac attribute, which is created based on the birthday attribute of the current model and returns a zodiac object.

#### Include Trait

```php
class User extends Model
{
    // include trait
    use \Intervention\Zodiac\Laravel\Traits\CanResolveZodiac;
    
    // optional: If you want overwrite attribute. By default `birthday`
    protected $birthdayAttribute = 'date_of_birth';
}
```

#### Zodiac Attribute

```php
// retrieve zodiac attribute
$user = App\User::create(['birthday' => '1980-03-15']);
$zodiac = $user->zodiac; // Intervention\Zodiac\Zodiacs\Pisces
```
