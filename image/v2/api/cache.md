# cache — Create cached images

## Description

> public Intervention\Image\ImageManager cache( Closure $callback, [int $lifetime, [bool $returnObj]] )

Method to create a new cached image instance from a **Closure callback**. Pass a **lifetime** in minutes for the callback and decide whether you want to get an Intervention Image instance as **return value** or just receive the image stream.

**Note: This method requires the additional package intervention/imagecache.**

## Parameters

### callback
A closure containing the operations on an image, defining the cached image.

### lifetime (optional)
The lifetime in minutes of the image callback in the cache. (Default: 5)

### returnObj (optional)
Decide if you want the method to return an Intervention Image instance or (by default) the image stream.

## Return Values
Mixed - based on ```returnObj``` parameter.

## Examples

```php
// create a cached image and set a lifetime and return as object instead of string
$img = Image::cache(function($image) {
   $image->make('public/foo.jpg')->resize(300, 200)->greyscale();
}, 10, true);
```


## See also
- [Further Information about Image Caching](/use/cache)