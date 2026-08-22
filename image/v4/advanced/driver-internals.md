---
title: "Driver Internals"
subtitle: "Access driver's native image data"
lead: "Advanced Intervention Image techniques: access native image data directly and combine with custom modifier classes for complex transformations."
sort: 3
---

[TOC]

If the supplied options are not sufficient, you can create your own
solutions using your own [custom extensions](/v4/modifying-images/custom-extensions).
Furthermore, you can access the native image object, so that all functions
used by the actual image processing libraries (such as GD or Imagick) can
be used — even those not covered by Intervention Image.

## Access the Native Image Object

Depending on the driver, each image object is mapped internally by either an
instance of a `GDImage::class` or an `Imagick::class` object. The parent image object of
Intervention Image provides access to this base object.

The following example uses the native Imagick function [oilPaintImage()](https://www.php.net/manual/en/imagick.oilpaintimage.php) which is not included in this library.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// read test image from a file
$image = ImageManager::usingDriver(Driver::class)->decode('test.png');

// access Imagick instance directly
$imagick = $image->core()->native();

// use Imagick method
$imagick->oilPaintImage(4.5);
```

Combined with [custom extensions](/v4/modifying-images/custom-extensions), Intervention
Image can be extended with your own modifier combinations for endless
possibilities.
