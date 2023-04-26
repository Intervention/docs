# Installation
## Easy installation via Composer

[TOC]

### System Requirements

Intervention Image requires the following components to work correctly.

- PHP >= 5.4
- Fileinfo Extension

And **one of** the following image libraries.

- GD Library (>=2.0) &hellip; **or** &hellip;
- Imagick PHP extension (>=6.5.7)

## Installation

The best way to install Intervention Image is quickly and easily with [Composer](https://getcomposer.org/).

To install the most recent version, run the following command.

```bash
$ php composer.phar require intervention/image
```

Now your ```composer.json``` has been updated automatically and you're able to require the just created ```vendor/autoload.php``` file to PSR-4 autoload the library.

The next step is to decide, if you want to integrate Intervention Image into the **Laravel framework**. If you want to use the library with Laravel, just skip the following step and continue with the description of [Laravel Integration](#integration-in-laravel).


## Usage

Intervention Image doesn't require Laravel or any other framework at all. If you want to use it as is, you just have to require the composer autoload file to instantiate image objects as shown in the following example.

#### Example

```php
// include composer autoload
require 'vendor/autoload.php';

// import the Intervention Image Manager Class
use Intervention\Image\ImageManager;

// create an image manager instance with favored driver
$manager = new ImageManager(['driver' => 'imagick']);

// to finally create image instances
$image = $manager->make('public/foo.jpg')->resize(300, 200);
```

You might also use the static version of ImageManager as shown in the example below.

#### Static Example

```php
// include composer autoload
require 'vendor/autoload.php';

// import the Intervention Image Manager Class
use Intervention\Image\ImageManagerStatic as Image;

// configure with favored image driver (gd by default)
Image::configure(['driver' => 'imagick']);

// and you are ready to go ...
$image = Image::make('public/foo.jpg')->resize(300, 200);
```

<a name="laravel"></a>
## Integration in Laravel 

Intervention Image has optional support for [Laravel](https://www.laravel.com) and comes with a **Service Provider and Facades** for easy integration. The `vendor/autoload.php` is included by Laravel, so you don't have to require or autoload manually. Just see the instructions below.

After you have installed Intervention Image, open your Laravel config file ```config/app.php``` and add the following lines.

In the ```$providers``` array add the service providers for this package.

```
Intervention\Image\ImageServiceProvider::class
```

Add the facade of this package to the ```$aliases``` array.

```php
'Image' => Intervention\Image\Facades\Image::class
```

Now the Image Class will be auto-loaded by Laravel.


### Configuration

By default Intervention Image uses PHP's GD library extension to process all images. If you want to switch to Imagick, you can pull a configuration file into your application by running one of the following artisan command.

#### Publish configuration in Laravel

```bash
$ php artisan vendor:publish --provider="Intervention\Image\ImageServiceProviderLaravelRecent"
````


#### Publish configuration in Laravel <= 4

```bash
$ php artisan config:publish intervention/image
```
In recent Laravel applications the configuration file is copied to `config/image.php`, in older Laravel 4 applications you will find the file at ```app/config/packages/intervention/image/config.php```. With this copy you can alter the image driver settings for you application locally.

#### Example

```php
// usage inside a laravel route
Route::get('/', function() {
    $img = Image::make('foo.jpg')->resize(300, 200);
    return $img->response('jpg');
});
```


