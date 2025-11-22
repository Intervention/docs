---
title: "Framework Integration"
subtitle: "Integration in Laravel"
lead: "Explore how to integrate Intervention Zodiac with the Laravel framework. Learn to set up configuration files and use the calculator via static facades."
sort: 3
---

[TOC]

## Laravel

Intervention Zodiac comes with Laravel facades ...

### Application-wide Configuration

A global configuration file that is recognized by Laravel is included. It is
therefore possible to configure a default setting for the astrology to be used
by the calculator facade.

The configuration file can be copied to the application with the following command.

```bash
php artisan vendor:publish --provider="Intervention\Zodiac\Laravel\ServiceProvider"
```

This command will publish the configuration file `config/zodiac.php` to your local 
applications config folder. Here you can set the default astrology type to be used for
calculations.

### Static Facade Interface

This package also integrates access to the central entry point `Intervention\Zodiac\Calculator::class`, via a static [facade](https://laravel.com/docs/facades). 

The following code example shows how to calculate a zodiac sign via the zodiac facade in a Laravel application.

```php
use Illuminate\Http\Request;
use Intervention\Zodiac\Laravel\Facades\Zodiac;

Route::get('/', function (Request $request) {
    $sign = Zodiac::fromString($request->input('date'));
});
```
