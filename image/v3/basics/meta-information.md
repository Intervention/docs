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

> public Image::height(): integer

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

// read image size
$size = $image->size();

// read aspect ratio
$ratio = $size->aspectRatio();

// read width from size
$width = $size()->width();
```

## Image Resolution

### Reading the image resolution

> public Image::resolution(): ResolutionInterface

Reads out the image resolution of the current instance in DPI.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading an image
$image = $manager->read('images/example.png');

// read image resolution object
$resolution = $image->resolution();

// convert resolution to dpcm
$resolution = $resolution->perCm();

// read resolution for each axis
$x = $resolution->x();
$y = $resolution->y();
```

### Set the image resolution

> public Image::setResolution(float $x, float $y): ImageInterface

Set the image resolution in DPI for each axis. Please note that the resolution
is encoded only for image formats that support this feature.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | float | Resolution on the x-axis |
| y | float | Resolution on the y-axis |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// read an image
$image = $manager->read('images/example.jpg');

// set image resolution to 300 DPI 
$image->setResolution(300, 300);
```


## Color Information

### Reading colors of certain pixels

> public Image::pickColor(int $x, int $y, int $frame_key = 0): ColorInterface

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

// 'rgb(243, 251, 230)'
$string = $color->toString();

// (int) 243
$red = $color->red()->toInt();

// (int) 251
$green = $color->green()->toInt();

// (int) 230
$blue = $color->blue()->toInt();

// (int) 255
$alpha = $color->alpha()->toInt();
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

## Colorspaces

The supported colorspaces primarily depend on the driver used. While the
library supports with Imagick driver RGB and CMYK colorspaces, the GD driver
is limited to the RGB colorspace.

If you are reading CMYK images with Intervention Image using the GD driver the
images are transformed to RGB colorspace automatically.

### Reading the Colorspace

> public Image::colorspace(): ColorspaceInterface

This function reads the colorspace from the current image instance.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// reading an image
$image = $manager->read('images/example.jpg');

// read the colorspace object
$colorspace = $image->colorspace();
```

### Changing the Colorspace

> public Image::setColorspace(string|ColorspaceInterface $colorspace): ImageInterface

This function transforms the current image into the given colorspace. The
target colorspace can be specified either as a colorspace object, as a class
name, or as an abbreviation for the colorspace.

#### Parameters

| Name | Type | Description |
| - | - | - |
| colorspace | string or ColorspaceInterface | Target colorspace |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Colors\Rgb\Colorspace as RgbColorspace;
use Intervention\Image\Colors\Cmyk\Colorspace as CmykColorspace;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// reading an image
$image = $manager->read('images/example.jpg');

// transform image to CMYK
$colorspace = $image->setColorspace('cmyk');

// transform image to rgb again
$colorspace = $image->setColorspace(RgbColorspace::class);

// and transform to cmyk again
$colorspace = $image->setColorspace(new CmykColorspace());
```

## Color Profiles

Currently Intervention Image is only able to handle color profiles with the
`ìmagick` driver.

### Reading Color Profiles

> public Image::profile(): ProfileInterface

This function reads the ICC color profile from the current image instance. If
no profile is found an `ColorException` is thrown.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// reading an image
$image = $manager->read('images/example.jpg');

// read the icc profile
$profile = $image->profile();

// save profile in file system
$profile->save('my_profile.icc')
```

### Writing Color Profiles

> public function setProfile(string|ProfileInterface $input): ImageInterface

This function set a given ICC color profile to the current image instance.
Usually the function takes the pathname of the profile, but it can also process
an object that implements the ProfileInterface.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// reading an image
$image = $manager->read('images/example.jpg');

// set the new color profile
$image->setProfile('profiles/profile.icc');
```

## Exif Information

Currently Intervention Image is only able to read Exif information. The
possibility to change certain information blocks is not implemented.

### Reading Exif information

> public Image::exif(?string $query = null): mixed

This function reads Exif information from the current image instance. You have
the option to pass a parameter to read a specific block of information from the
Exif data directly. If no parameter is passed, all data will be returned. If
the specified block is not found, `null` is returned as result.

#### Parameters

| Name | Type | Description |
| - | - | - |
| query | string or null | Optionally query exif information block directly |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading an image
$image = $manager->read('images/example.jpg');

// read the specific exif data
$camera = $image->exif('IFD0.Model');

// read all exif information
$all = $image->exif();

// the exif data block can be queried as well
$camera = $all->get('IFD0.Model');
```
