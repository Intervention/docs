# Image Caching
## Image Caching

The optional package [Intervention Image Cache](https://packagist.org/packages/intervention/imagecache) extends the package to be capable of image caching.

The caching library uses the [Illuminate/Cache](https://github.com/illuminate/cache/) package which is part of Laravel and can be easily integrated into the [Laravel Framework](http://laravel.com). Based on your Laravel cache configuration you are able to choose between Filesystem, Database, Memcached or Redis for the temporary buffer store.

The principle is simple. Once the caching package is installed, you are able to call the static cache method. Every method call to the Intervention Image class is captured and checked by the caching interface. If this particular sequence of operations already have taken place, the data will be loaded directly from the cache instead of a resource-intensive GD operation.

## Installation

Require the caching package via Composer by running the following command:

> $ php composer.phar require intervention/imagecache

Now you are able to require the vendor/autoload.php file to PSR-4 autoload the library.

## Usage

Simply pass every manipulation operation as a Closure callback:

```php
// pass calls to image cache
$img = Image::cache(function($image) {
    $image->make('public/foo.jpg')->resize(300, 200)->greyscale();
});
```

Read the [cache()](/api/cache) method documentation to find out more about the possibilities.

To take the caching one step further, take a look at [URL based image manipulation](/usage/url-manipulation).