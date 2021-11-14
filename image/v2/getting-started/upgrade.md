# Upgrading from 1.x to 2.x

Although I tried to keep the update to Version 2.x of Intervention Image as compatible as possible, some things have changed. Some methods became redundant, other things have been simplified and therefore had to change. 

## New Features

- Additional support of PHP's Imagick extension
- Sharpening Images
- Auto Orientating
- Image Filter architecture

In order to keep your application compatible, you need to keep in mind the following changes, when upgrading.

### New Methods

* [width()](/api/width) retrieves current width of image.
* [height()](/api/height) retrieves current height of image.
* [sharpen()](/api/sharpen) applies sharpen filter to image.
* [orientate()](/api/orientate) auto-adjusts image orientation.
* [filter()](/api/filter) applies filter to an image.
* [getCore()](/api/getCore) get resource of image driver (Imagick object or GD resource).

### Changed Method names

* [fit()](/api/fit) replaces the old ```grab()``` method.

### Changed Arguments on methods

* Method [gamma()](/api/gamma) now only accepts one argument for gamma correction. 
* Changed arguments for [resize()](/api/resize) method. Now uses callback to define further options. 
* Changed arguments for [circle()](/api/circle) method. Now uses callback to define further options.
* Changed arguments for [ellipse()](/api/ellipse) method. Now uses callback to define further options.
* Changed arguments for [line()](/api/line) method. Now uses callback to define further options.
* Changed arguments for [rectangle()](/api/rectangle) method. Now uses callback to define further options.

### Removed methods

* ```open()``` no longer exists, use [make()](/api/make) instead.
* ```raw()``` no longer exists, use [make()](/api/make) instead.
* ```grayscale()``` no longer exists, use [greyscale()](/api/greyscale) instead.

### Removed properties

* ```width``` property has been removed, use [width()](/api/width) instead.
* ```height``` property has been removed, use [height()](/api/height) instead.

### Other

* To keep naming consistent the filename of the configuration file for *intervention/imagecache* was renamed from `config/imagecache.php` to `config/config.php`.
* For standalone use instantiate objects from `Intervention\Image\ImageManagerStatic` instead of `Intervention\Image\Image`. ([See example](/getting_started/installation))
