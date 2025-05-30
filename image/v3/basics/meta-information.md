---
label: "Meta Information"
title: "Meta Information"
subtitle: "Read Meta Data from Images"
lead: "Discover how to manage meta information in images with Intervention Image. Learn to read image dimensions, resolution, and Exif data, including pixel sizes, DPI settings, and camera metadata."
sort: 2
---

[TOC]

## Image Sizes

### Read the Pixel Width

> public Image::width(): integer

Read the pixel width in pixels from an instance.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an image
$image = $manager->read('images/example.png');

// read the image width
$width = $image->width();
```

### Read the Pixel Height

> public Image::height(): integer

Read the pixel height from an image instance.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an image
$image = $manager->read('images/example.png');

// read the image height
$height = $image->height();
```

### Read the Image Size as an Object

> public Image::size(): SizeInterface

Read the pixel size from an image instance.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// read an image
$image = $manager->read('images/example.png');

// read image size
$size = $image->size();

// read aspect ratio
$ratio = $size->aspectRatio();

// determine image format
$is_portrait = $size->isPortrait(); // true
$is_landscape = $size->isLandscape(); // false

// read width from size
$width = $size()->width();
```

## Image Resolution

### Read the Image Resolution

> public Image::resolution(): ResolutionInterface

Reads out the image resolution of the current instance in DPI.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// read an image
$image = $manager->read('images/example.png');

// read image resolution object
$resolution = $image->resolution();

// convert resolution to dpcm
$resolution = $resolution->perCm();

// read resolution for each axis
$x = $resolution->x();
$y = $resolution->y();
```

### Set the Image Resolution

> public Image::setResolution(float $x, float $y): ImageInterface

Set the image resolution in DPI for each axis. Please note that the resolution
is encoded only for image formats that support this feature.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | float | Resolution on the x-axis |
| y | float | Resolution on the y-axis |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an image
$image = $manager->read('images/example.jpg');

// set image resolution to 300 DPI 
$image->setResolution(300, 300);
```


## Exif Information

Currently Intervention Image is only able to read Exif information. The
possibility to write Exif data blocks is not implemented.

### Read Exif Information

> public Image::exif(null|string $query = null): mixed

This function reads Exif information from the current image instance. You have
the option to pass a parameter to read a specific block of information from the
Exif data directly. If no parameter is passed, all data will be returned. If
the specified block is not found, `null` is returned as result.

**To use this function, the PHP Exif extension must be installed.**

#### Parameters

| Name | Type | Description |
| - | - | - |
| query | string or null | Optionally query exif information block directly |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an image
$image = $manager->read('images/example.jpg');

// read the specific exif data
$camera = $image->exif('IFD0.Model');

// read all exif information
$all = $image->exif();

// the exif data block can be queried as well
$camera = $all->get('IFD0.Model');
```
