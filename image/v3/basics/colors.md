---
label: "Colors & Transparency"
title: "Colors & Transparency"
subtitle: "Handling of Image Colors"
lead: "Explore advanced image color handling and transparency management with Intervention Image. Learn how to read and transform pixel colors, manage colorspaces, work with ICC profiles, and blend transparency for dynamic image processing."
sort: 3
---

[TOC]

## Color Information

### Read Colors of Certain Pixels

> public Image::pickColor(int $x, int $y, int $frame_key = 0): ColorInterface

Reads the color of the pixel specified by the X and Y coordinates. You can also
get the key of the frame from which the color is taken. This is only relevant
for animated images.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | int | X-Coordinate of the pixel position |
| y | int | Y-Coordinate of the pixel position |
| frame_key | int | Optional key of the frame from which the color information is read |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

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

### Read all Colors of Certain Pixels in Animated Images

> public Image::pickColors(int $x, int $y): CollectionInterface

Reads all colors of the pixel specified via the X and Y coordinates and returns
them in a collection. For animated images, this collection will contain all
colors of the specified position for all frames. For non-animated images, the
collection will contain only one color, because the image also contains only one
frame.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | int | X-Coordinate of the pixel position |
| y | int | Y-Coordinate of the pixel position |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an image
$image = $manager->read('images/animation.gif');

// read color information at position
$colors = $image->pickColors(10, 10);

// first color
$color = $colors->first();

// color for certain frame
$color = $colors->get(6);
```

## Transforming Colors

Once the pixel colors of an image have been read into an object, more options are available.

### Transform Colors to String Values

> public ColorInterface::toString(): ColorInterface

Each color object can also be output as a string. You can use the `toString()`
method or to cast the object directly. Of course, the output depends on the
respective color space.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Colors\Hsl\Colorspace as HslColorspace;

// create new manager instance with desired driver
$manager = ImageManager::gd();

// read an image
$image = $manager->read('images/example.png');

// read pixel color
$color = $image->pickColor(20, 10);

// transform color to string format
$result = $color->toString(); // "rgba(255, 255, 255, 1.0)"

// same result
$result = (string) $color;
```


### Transform Colors Between Colorspaces

> public ColorInterface::convertTo(string|ColorspaceInterface $colorspace): ColorInterface

Each color object has a method for converting into other color spaces. The
target color space can be specified either as a string or as an object. This
works even if the current driver does not support the target color space.

The following color spaces are available.

- `Intervention\Image\Colors\Rgb\Colorspace`
- `Intervention\Image\Colors\Cmyk\Colorspace`
- `Intervention\Image\Colors\Hsv\Colorspace`
- `Intervention\Image\Colors\Hsl\Colorspace`

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Colors\Hsl\Colorspace as HslColorspace;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// read an image
$image = $manager->read('images/example.png');

// read pixel color
$color = $image->pickColor(20, 10);

$result = $color->toString(); // "rgba(0, 255, 255, 1.0)"

// transform color to hsl format
$hslColor = $color->convertTo(HslColorspace::class);

$result = $hslColor->toString(); // "hsl(180, 100, 50)"
```

## Colorspaces

The supported colorspaces depend mainly on the driver used. While the
Imagick driver supports RGB and CMYK colorspace, the GD driver
is limited to the RGB colorspace.

When reading CMYK images with Intervention Image using the GD driver the
images are automatically converted to RGB colorspace.

### Read the Image Colorspace

> public Image::colorspace(): ColorspaceInterface

This function reads the colorspace of the current image instance.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading an image
$image = $manager->read('images/example.jpg');

// read the colorspace object
$colorspace = $image->colorspace();
```

### Change the Image Colorspace

> public Image::setColorspace(string|ColorspaceInterface $colorspace): ImageInterface

This function converts the current image to the specified colorspace. The
target colorspace can be specified either as an object, as a class
name, or as an abbreviation of the colorspace.

#### Parameters

| Name | Type | Description |
| - | - | - |
| colorspace | string or ColorspaceInterface | Target colorspace |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Colors\Rgb\Colorspace as RgbColorspace;
use Intervention\Image\Colors\Cmyk\Colorspace as CmykColorspace;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an image
$image = $manager->read('images/example.jpg');

// transform image to CMYK by abbreviation
$colorspace = $image->setColorspace('cmyk');

// transform image to rgb again by class name
$colorspace = $image->setColorspace(RgbColorspace::class);

// and transform to cmyk again by object
$colorspace = $image->setColorspace(new CmykColorspace());
```

## Color Profiles

Currently Intervention Image can only handle color profiles with the `ìmagick` driver.

### Read Color Profiles

> public Image::profile(): ProfileInterface

This function reads the ICC color profile from the current image instance. If
no profile is found an `ColorException` is thrown.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an image
$image = $manager->read('images/example.jpg');

// read the icc profile
$profile = $image->profile();

// save profile in file system
$profile->save('my_profile.icc')
```

### Set Color Profiles

> public function setProfile(ProfileInterface $profile): ImageInterface

This function applies a given ICC color profile to the current image instance.
The function takes an instance of `ProfileInterface::class` as an argument.

#### Parameters

| Name | Type | Description |
| - | - | - |
| profile | ProfileInterface | Target icc profile |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Colors\Profile;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading an image
$image = $manager->read('images/example.jpg');

// set the new color profile
$image->setProfile(Profile::fromPath('profiles/profile.icc'));
```

### Remove Color Profiles

> public function removeProfile(): ImageInterface

Removes all color profiles from the current image.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// read image and remove profile
$image = $manager->read('images/example.jpg')->removeProfile();
```

## Transparency

Intervention Image supports image formats with alpha channels. Transparent
areas are preserved as long as the output format supports transparency.

If the output format does not support transparency, no alpha channel can be
preserved. In this case the transparent areas will be blended with an opaque color.
This color can be specified in advance in the initial [configuration of the
image manager](/v3/basics/configuration-drivers) or as an optional argument in the following
method. It is also possible to set or get the blending color at runtime.

### Merge Transparent Areas with Color

> public function blendTransparency(mixed $color = null): ImageInterface

When switching to a non-transparent image format, the transparency is
automatically replaced with the [configured blending
color](/v3/basics/configuration-drivers), but this can also be done manually. This
function call can also be applied to image formats that can actually contain
transparency.

The `color` parameter can optionally be used to specify a color in the common
[color formats](/v3/getting-started/formats#color-formats). By default, this is
the current or previously configured blending color. Note that any transparency
values in the blend color will be ignored.

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | mixed | Color to replace transparent areas (optional). |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver and default blending color
$manager = new ImageManager(Driver::class);

// read a transparent image
$image = $manager->read('images/example.png');

// merge the transparent areas with orange
$image->blendTransparency('f50');
```

### Read the Blending Color

> public function blendingColor(): ColorInterface

Return the currently set blending color as an instance of
`ColorInterface::class`. This corresponds either to the color originally
configured through the ImageManager or the blending color that was last set.

### Set the Blending Color

> public function setBlendingColor(mixed $color): ImageInterface

Set a new blending color in the configuration of the current image instance.
This color will be used as the default for all subsequent operations that use a
blend color, overwriting the original value defined in the ImageManager
configuration.

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | mixed | New blending color in supported [color formats](/v3/getting-started/formats#color-formats). |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver and red as blending color
$manager = new ImageManager(Driver::class, blendingColor: 'ff0000');

// read image
$image = $manager->read('images/example.png');

// read configured blending color
$blendingColor = $image->blendingColor(); // 'ff0000'

// set grey as blending color
$image->setBlendingColor('cccccc');

// read last set blending color
$blendingColor = $image->blendingColor(); // 'cccccc'
