# Framework Integration
## Use Intervention Image with your favorite framework

[TOC]

## Laravel

Intervention Image can be easily integrated into a Laravel application with the
official bundle. This package provides a Laravel service provider, facade and a
publishable configuration file.

Although this integration is not mandatory, it has the advantage of integrating
the configuration centrally in the application.

### Integration

Instead of installing the library directly, it is only necessary to integrate
the bundle. The corresponding basic libraries are automatically installed as
well

```bash
$ composer require intervention/image-laravel
```

Next, add the configuration files to your application using the `vendor:publish` command:

```bash
php artisan vendor:publish --provider="Intervention\Image\Laravel\ServiceProvider"
```

This command will publish the configuration file `image.php` for the image
integration to your `app/config` directory. In this file you can set the desired
driver for Intervention Image. By default the library is configured to use GD
library for image processing.

The integration is now complete and it is possible to access the
[ImageManager](/v3/basics/instantiation) via
Laravel's facade.

```php
use Intervention\Image\Laravel\Facades\Image;

Route::get('/', function () {
    $image = Image::create(300, 200);
});
```
