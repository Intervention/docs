---
title: "Intervention Image"
label: "Introduction"
subtitle: "PHP Image Processing"
lead: "Intervention Image is the most popular open source PHP image processing library. It provides an easy and expressive way to edit images and supports PHP's three most common image processing libraries GD Library, Imagick or libvips."
sort: 0
---

### Features

- Fluent API for common image editing tasks
- Interchangable driver architecture for all popular PHP image processing extensions
- Support for GD, Imagick and [libvips](https://github.com/Intervention/image-driver-vips)
- Processing of animated images with all drivers
- Support for colorspaces and profiles
- Support for text wrapping and line height in the font system

The library is written to make PHP image manipulation easy and effortless.
Whether you want to create image thumbnails, set watermarks, or format large
image files, Intervention Image helps you accomplish any task with just a few
lines of code. 

### Code Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Alignment;
use Intervention\Image\Color;
use Intervention\Image\Format;
use Intervention\Image\Fraction;

// create image manager instance using the desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read image data from path
$image = $manager->decodePath('images/example.webp');

// scale image by height
$image->scale(height: 300);

// insert a watermark
$image->insert('images/watermark.png', alignment: Alignment::BOTTOM_RIGHT);

// encode edited image
$encoded = $image->encodeUsingFormat(Format::JPEG, quality: 65);

// save encoded image
$encoded->save('images/example.jpg');
```

The library follows the FIG PSR-12 standard to ensure a high level of
interoperability between shared PHP code and is fully unit tested.

Read how to [install Intervention Image](/v4/getting-started/installation) or take a look at the [live demo](/v4/playground) to try the results of resizing functions directly.
