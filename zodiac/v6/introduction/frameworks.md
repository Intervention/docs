---
title: "Framework Integration"
subtitle: "Integration in Laravel"
lead: "Explore how to integrate Intervention Zodiac with the Laravel framework. Learn to set up configuration files, select drivers and leverage features like auto-orientation, decoding animations, and blending color."
sort: 2
---

[TOC]

## Laravel

Intervention Zodiac comes with Laravel facades ...

### Static Facade Interface

This package also integrates access to the central entry point `Intervention\Zodiac\Calculator::class`, via a static [facade](https://laravel.com/docs/facades). 

The following code example shows how to calculate a zodiac sign via the zodiac facade in a Laravel application.

```php
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Route;
use Illuminate\Support\Facades\Storage;
use Illuminate\Support\Str;
use Intervention\Zodiac\Laravel\Facades\Zodiac;

Route::get('/', function (Request $request) {
    $sign = Image::western()->fromString($request->input('date'));
});
```
