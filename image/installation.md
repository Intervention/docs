# Installation

The best way to install Intervention Image is quickly and easily with [Composer](http://getcomposer.org/) via [Packagist](https://packagist.org/packages/intervention/image).

Require the package via Composer in your ```composer.json```.

> "intervention/image": "2.*"

Run Composer to install or update the new requirement.

> $ php composer.phar install

or

> $ php composer.phar update

Now you are able to require the vendor/autoload.php file to PSR-0 autoload the library.

## Example

```php
// include composer autoload
require 'vendor/autoload.php';

// import the Intervention Image Manager Class
use Intervention\Image\ImageManagerStatic as Image;

// and your are ready to go ...
$image = Image::make('public/foo.jpg')->resize(300, 200);
```


The Image class also has optional **Laravel 4 support**. The integration into the framework is done in seconds.

Read more about [Laravel 4 integration](laravel).

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
