# Installation
## Installing Intervention Image

[TOC]

## Server Requirements

Before you begin with the installation make sure your server environment
supports the following requirements.

- PHP >= 8.1
- A PHP image processing extension

### Image Processing Extension

Depending on your PHP installation Intervention Image lets you choose between
two different image processing libraries.

[GD Image](https://www.php.net/manual/en/book.image.php) or
[ImageMagick](https://www.php.net/manual/en/book.imagick.php) are the most
popular image processing libraries for PHP. Your server environment must
support at least one of them. GD is part of most PHP installations. However I
recommend using ImageMagick because I think it is faster and more efficient
especially for larger images.

## Installation

The best way to install Intervention Image is quickly and easily with
[Composer](https://getcomposer.org/).

**This is an early beta version and should installed for development and testing only.**

First make sure to allow unstable releases by setting the `minimum-stability`
value on your `composer.json` to `beta`. Then continue by running the following
command.

```bash
$ composer require intervention/image ^3.0@beta
```

Your `composer.json` will be updated automatically and you're able use the
classes of the package via the autoloader. To do so require the just created
`vendor/autoload.php` file to PSR-4 autoload all your installed composer
packages.

After installation you can start to [use the library](/v3/basics/instantiation).
