# Intervention Image
## PHP Image Manipulation

## Introduction

Intervention Image is the most popular open source **PHP image manipulation library**. It provides an easy and expressive way to edit images and supports the two most common image processing libraries **GD Library** and **Imagick**.

### Features

- Support for GD & Imagick
- Manipulation of animated images
- Improved architecture
- PSR-12 standardized

The library is written to make PHP image manipulating easy and effortless. No matter if you want to create image thumbnails, set watermarks or format large image files Intervention Image helps you to manage every task with as little lines of code as possible.

With version 3, the proven features have been improved and unique new details have been added. 

### Code Example

```php
use Intervention\Image\ImageManager;

// create image manager with desired driver
$manager = new ImageManager('imagick');

// read image from file system
$image = $manager->make('images/example.jpg');

// resize image proportionally to 300px width
$image->scale(width: 300);

// insert watermark
$image->place('images/watermark.png');

// save modified image in new format 
$image->toPng()->save('images/foo.png');

```

The library follows the FIG standard PSR-12 to ensure a high level of interoperability between shared PHP code and is fully unit-tested.

Read how to [install Intervention Image](/).