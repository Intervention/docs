# Configuration
## Set up Intervention Image

[TOC]

## Driver Configuration

Currently Intervention Image supports two Image processing extensions. Make sure you have one of these installed in your PHP environment, before you start.

- **GD**
- **Imagick**

You're able to configure Intervention Image to use one of these libraries for all its operations. Just pass the configuration as an array directly into the ImageManager.

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

## Memory Settings

Image manipulation in PHP is a very memory consuming task. Since most tasks in PHP don't exhaust default memory limits, you have to make sure your PHP configuration is able to allocate enough memory to handle large images.

The following php.ini directives are important.

### memory_limit

Sets a maximum amount of memory in bytes that a script is allowed to allocate. Resizing a 3000 x 2000 pixel image to 300 x 200 may take up to 32MB memory.

### upload_max_filesize

If you're planing to upload large images, verify that this setting for the maximum size of file uploads fits your needs.

Read more in the official PHP documentation for:

* [memory_limit](http://www.php.net/manual/en/ini.core.php#ini.memory-limit)
* [upload_max_filesize](http://www.php.net/manual/en/ini.core.php#ini.upload-max-filesize)

It's possible to set these directives in your [php.ini](http://www.php.net/manual/en/ini.core.php) or at runtime with [ini_set](http://www.php.net/manual/en/function.ini-set.php).



## Configuration in Laravel

If you're using Laravel, you can pull a configuration file into your application by running the following artisan command.

### Publish configuration in Laravel 5

> $ php artisan vendor:publish

### Publish configuration in Laravel 4

> $ php artisan config:publish intervention/image

In Laravel 5 applications the configuration file is copied to ```config/image.php```, in older Laravel 4 applications you will find the file at ```app/config/packages/intervention/image/config.php```. With this copy you can alter the image driver settings for you application locally and define which library should be used by all commands..

```php
'driver' => 'imagick'
```

Currently you can choose between `gd` and `imagick` support.
