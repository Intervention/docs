# Meta Information
## Reading meta data from images

[TOC]

## Image Sizes

### Reading the pixel width

> public Image::width(): integer

Reading the width in pixels from an image instance.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->read('images/example.png');

// reading the image width
$width = $image->width();
```

### Reading the pixel height

> public Image::width(): integer

Reading the pixel height from an image instance.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->read('images/example.png');

// reading the image height
$height = $image->height();
```

### Reading the image size as an object

> public Image::size(): SizeInterface

Reading the image size from an instance.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->read('images/example.png');

// reading image size
$size = $image->size();

// read aspect ratio
$ratio = $size->getAspectRatio();
```

## Exif Information

Currently Intervention Image is only able to read Exif information. The
possibility to change certain information blocks is not implemented.

### Reading Exif information

> public Image::getExif(?string $query = null): mixed

This function reads Exif information from the current image instance. You have
the option to pass a parameter to read a specific block of information from the
Exif data directly. If no parameter is passed, all data will be returned. If
the specified block is not found, `null` is returned as result.

#### Parameters

| Name | Type | Description |
| - | - | - |
| query | string|null | Optionally query exif information block directly |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->read('images/example.jpg');

// read the specific exif data
$camery = $image->getExif('IFD0.Model');

// read all exif information
$all = $image->getExif();

// the exif data block can be queried as well
$camera = $all->get('IFD0.Model');
```
