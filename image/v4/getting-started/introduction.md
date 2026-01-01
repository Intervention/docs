---
title: "Intervention Image"
label: "Introduction"
subtitle: "PHP Image Processing"
lead: "Intervention Image is the most popular open source PHP image processing library. It provides an easy and expressive way to edit images and supports PHP's three most common image processing libraries GD Library, Imagick or libvips."
sort: 0
---

### Features

- Fluent & unified API for GD, Imagick or [libvips](https://github.com/Intervention/image-driver-vips)
- Processing of animated Images
- Support for colorspaces and profiles
- Support for text wrapping and line height in the font system
- Improved architecture
- PSR-12 standardized

The library is written to make PHP image manipulation easy and effortless.
Whether you want to create image thumbnails, set watermarks, or format large
image files, Intervention Image helps you accomplish any task with just a few
lines of code. 

Version 4 improves the solid library even further and adds unique new features.

### Code Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\Image\Alignment;
use Intervention\Image\Color;
use Intervention\Image\Format;
use Intervention\Image\Fraction;

// create image manager with desired driver
$manager = ImageManager::withDriver(GdDriver::class);

// decode an image file
$image = $manager->decodeFromPath('images/example.webp');

// resize image width
$image->resize(width: 300);

// resize the image canvas
$image->resizeCanvas(height: Fraction::THIRD, background: Color::rgb(255, 55, 0));

// insert a watermark
$image->place('images/watermark.png', alignment: Alignment::CENTER);

// encode edited image
$encoded = $image->encodeUsing(format: Format::JPEG, quality: 65);

// save encoded image
$encoded->save('images/example.jpg');
```

The library follows the FIG PSR-12 standard to ensure a high level of
interoperability between shared PHP code and is fully unit tested.

Read how to [install Intervention Image](/v4/getting-started/installation) or take a look at the [live demo](/v4/playground) to try the results of resizing functions directly.
