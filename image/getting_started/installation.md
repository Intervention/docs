# Installation

## System Requirements

Intervention Image requires the following components to work correctly.

- PHP >= 5.3
- Fileinfo Extension

And one of the following image libraries.

- GD Library (>=2.0)
- Imagick PHP extension (>=6.3.8)

---

## Composer Installation

The best way to install Intervention Image is quickly and easily with [Composer](http://getcomposer.org/).

Require the package via Composer in your ```composer.json```.

> "intervention/image": "2.*"

Run Composer to install or update the new requirement.

> $ php composer.phar install

or

> $ php composer.phar update

Now you are able to require the new ```vendor/autoload.php``` file to PSR-0 autoload the library.

The next step is to decide, if you want to integrate Intervention Image into the **Laravel framework**. If you don't want to use the library with Laravel, just skip the following step and continue with the description of **native usage**.

---

<a name="laravel"></a>
## Laravel Usage

Intervention Image has optional support for [Laravel 4](http://laravel.com) and comes with a **Service Provider and Facades** for easy integration. The `vendor/autoload.php` is included by Laravel, so you don't have to require it again. Just see the instructions below.

After you have installed Intervention Image, open your Laravel config file ```config/app.php``` and add the following lines.

In the ```$providers``` array add the service providers for this package.

> 'Intervention\Image\ImageServiceProvider'

Add the facade of this package to the ```$aliases``` array.

> 'Image' => 'Intervention\Image\Facades\Image'

Now the Image Class will be auto-loaded by Laravel.


### Configuration

By default Intervention Image uses PHP's GD library extension to process all images. If you want to switch to Imagick, you can pull a configuration file into your application by running the following artisan command.

> $ php artisan config:publish intervention/image

This command copies a configuration file to ```app/config/packages/intervention/image/config.php```, where you can alter the driver settings for you application locally.


---

## Native Usage

Intervention Image doesn't require Laravel or any other framework at all. If you want to use it as is, you just have to require the composer autoload file to instatiate image objects as shown in the following example.

#### Example

```php
// include composer autoload
require 'vendor/autoload.php';

// import the Intervention Image Manager Class
use Intervention\Image\ImageManager;

// create an image manager instance with favored driver
$manager = new ImageManager(array('driver' => 'imagick'));

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
Image::configure(array('driver' => 'imagick'));

// and you are ready to go ...
$image = Image::make('public/foo.jpg')->resize(300, 200);
```
