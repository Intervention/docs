# Intervention Image

## PHP Image Processing

## Introduction

Intervention Image is the most popular open source **PHP image processing
library**. It provides an easy and expressive way to edit images and supports
PHP's two most common image processing libraries **GD Library** and **Imagick**.

### Features

- Unified API for GD & Imagick
- Processing of animated Images
- Support for colorspaces and profiles
- Support for text wrapping and line height in the font system
- Improved architecture
- PSR-12 standardized

The library is written to make PHP image manipulation easy and effortless.
Whether you want to create image thumbnails, set watermarks, or format large
image files, Intervention Image helps you accomplish any task with just a few
lines of code. 

Version 3 improves on the solid features and adds unique new details.

### Code Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create image manager with desired driver
$manager = new ImageManager(new Driver());

// read image from file system
$image = $manager->read('images/example.jpg');

// resize image proportionally to 300px width
$image->scale(width: 300);

// insert watermark
$image->place('images/watermark.png');

// save modified image in new format 
$image->toPng()->save('images/foo.png');

```

The library follows the FIG PSR-12 standard to ensure a high level of
interoperability between shared PHP code and is fully unit tested.

Read how to [install Intervention Image](/v3/introduction/installation).
