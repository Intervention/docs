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
$manager = new ImageManager(['driver' => 'gd']);

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
$manager = new ImageManager(['driver' => 'gd']);

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
$manager = new ImageManager(['driver' => 'gd']);

// reading an image
$image = $manager->read('images/example.png');

// reading image size
$size = $image->size();

// read aspect ratio
$ratio = $size->getAspectRatio();
```

## Color Information

### Reading colors of certain pixels

> public Image::pickColor(int $x, int $y, int $frame_key = 0): ?ColorInterface

Reads the color of the pixel specified via the X and Y coordinates.
Furthermore, the key of the frame from which the color is taken can be
determined. However, this is only relevant for animated images.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | int | X-Coordinate of the pixel position |
| y | int | Y-Coordinate of the pixel position |
| frame_key | int | Optional key of the frame from which the color information is read |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// read an image
$image = $manager->read('images/animation.gif');

// read color information for frame 10 at position 23/9
$color = $image->pickColor(23, 9, 10);

// 'f3fbe6'
$hex = $color->toHex();

// (int) 243
$red = $color->red();

// (int) 251
$green = $color->green();

// (int) 230
$blue = $color->blue();

// (float) 1
$hex = $color->alpha();
```

### Reading all colors of certain pixels in animated images

> public Image::pickColors(int $x, int $y): CollectionInterface

Reads all colors of the pixel specified via the X and Y coordinates and passes
them in a collection. For animated images, this collection will contain all
colors of the specified position for all frames. For non-animated images, the
collection will contain only one color, since the image also contains only one
frame.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | int | X-Coordinate of the pixel position |
| y | int | Y-Coordinate of the pixel position |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// read an image
$image = $manager->read('images/animation.gif');

// read color information at position
$colors = $image->pickColors(10, 10);

// first color
$color = $colors->first();

// color for certain frame
$color = $colors->get(6);
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
$manager = new ImageManager(['driver' => 'gd']);

// reading an image
$image = $manager->read('images/example.jpg');

// read the specific exif data
$camery = $image->getExif('IFD0.Model');

// read all exif information
$all = $image->getExif();

// the exif data block can be queried as well
$camera = $all->get('IFD0.Model');
```
