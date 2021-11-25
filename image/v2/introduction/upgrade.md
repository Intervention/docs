# Upgrade Guide
## Upgrade from Intervention Image 1.x to 2.x

[TOC]

Although I tried to keep the update to Version 2.x of Intervention Image as compatible as possible, some things have changed. Some methods became redundant, other things have been simplified and therefore had to change. 

## New Features

- Additional support of PHP's Imagick extension
- Sharpening Images
- Auto Orientating
- Image Filter architecture

In order to keep your application compatible, you need to keep in mind the following changes, when upgrading.

### New Methods

- [width()](/v2/api/width) retrieves current width of image.
- [height()](/v2/api/height) retrieves current height of image.
- [sharpen()](/v2/api/sharpen) applies sharpen filter to image.
- [orientate()](/v2/api/orientate) auto-adjusts image orientation.
- [filter()](/v2/api/filter) applies filter to an image.
- [getCore()](/v2/api/getCore) get resource of image driver (Imagick object or GD resource).

## API changes

### Changed Method names

- [fit()](/v2/api/fit) replaces the old ```grab()``` method.

### Changed Arguments on methods

- Method [gamma()](/v2/api/gamma) now only accepts one argument for gamma correction. 
- Changed arguments for [resize()](/v2/api/resize) method. Now uses callback to define further options. 
- Changed arguments for [circle()](/v2/api/circle) method. Now uses callback to define further options.
- Changed arguments for [ellipse()](/v2/api/ellipse) method. Now uses callback to define further options.
- Changed arguments for [line()](/v2/api/line) method. Now uses callback to define further options.
- Changed arguments for [rectangle()](/v2/api/rectangle) method. Now uses callback to define further options.

### Removed methods

- ```open()``` no longer exists, use [make()](/v2/api/make) instead.
- ```raw()``` no longer exists, use [make()](/v2/api/make) instead.
- ```grayscale()``` no longer exists, use [greyscale()](/v2/api/greyscale) instead.

### Removed properties

- ```width``` property has been removed, use [width()](/v2/api/width) instead.
- ```height``` property has been removed, use [height()](/v2/api/height) instead.

### Other

- To keep naming consistent the filename of the configuration file for *intervention/imagecache* was renamed from `config/imagecache.php` to `config/config.php`.
- For standalone use instantiate objects from `Intervention\Image\ImageManagerStatic` instead of `Intervention\Image\Image`. ([See example](/v2/getting-started/installation))
