# Installation
## Installing Intervention Image

[TOC]

## Server Requirements

Before you begin with the installation make sure that your server environment
supports the following requirements.

- PHP >= 8.1
- Mbstring PHP Extension
- Image Processing PHP Extension

Although it is not a requirement, it is **highly recommended to have the Exif
PHP extension installed** as well. This is used, among other things, to correctly
display the orientation of images.

### Image Processing Extension

Depending on your PHP installation Intervention Image lets you choose between
two different image processing libraries.

- [GD Image](https://www.php.net/manual/en/book.image.php)
- [Imagick](https://www.php.net/manual/en/book.imagick.php)

Your server environment must support at least one of them. GD is part of most
PHP installations. However I recommend using Imagick because I think it is
faster and more efficient especially for larger images.

## Installation

Install Intervention Image with [Composer](https://getcomposer.org/) by running
the following command.

```bash
composer require intervention/image
```

This will install Intervention Image with the most recent version, your
`composer.json` is automatically updated and you will be able use the package's
classes via the autoloader. To do this you will need to require the just
created `vendor/autoload.php` file to PSR-4 autoload all your installed
composer packages.

```php
require './vendor/autoload.php';
 
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());
```

After installation you are ready to [use the image manager](/v3/basics/image-manager) and [read or create image instances](/v3/basics/instantiation).
