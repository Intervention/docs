# Colors + Transparency
## Handling of Image Colors

[TOC]

## Color Information

### Reading Colors of Certain Pixels

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

### Reading all Colors of Certain Pixels in Animated Images

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

As soon as the pixel colors of an image have been read into an object, further
options are available.

### Transforming Colors to String Values

> public ColorInterface::toString(): ColorInterface

Each color object can also be output as a string. It is possible to use the
`toString()` method or to cast the object directly. Of course, the output
depends on the respective color space.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Colors\Hsl\Colorspace as HslColorspace;

// create new manager instance with desired driver
$manager = ImageManager::gd();

// read an image
$image = $manager->read('images/example.png');

// read pixel color
$color = $image->pickColor(20, 10);

// transform color to hsl format
$result = $color->toString(); // "rgba(255, 255, 255, 1.0)"

// same result
$result = (string) $color;
```


### Transforming Colors Between Colorspaces

> public ColorInterface::convertTo(string|ColorspaceInterface $colorspace): ColorInterface

Each color object has a method for converting into other color spaces. Here,
the target space can be specified either as a string or as an object. This also
works if the driver used does not support the target color space.

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
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

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
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Colors\Rgb\Colorspace as RgbColorspace;
use Intervention\Image\Colors\Cmyk\Colorspace as CmykColorspace;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

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
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

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
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading an image
$image = $manager->read('images/example.jpg');

// set the new color profile
$image->setProfile('profiles/profile.icc');
```

### Removing Color Profiles

> public function removeProfile(): ImageInterface

Removes all color profiles from the current image.

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// read image and remove profile
$image = $manager->read('images/example.jpg')->removeProfile();
```

## Transparency

Intervention Image supports image formats with alpha channels during decoding
and output. Transparent areas are preserved as long as the destination format
supports transparency.

If the target format does not support transparency, no alpha channel can be
preserved. In this case the transparent areas will be blended with a color. This
color can be specified in advance.

### Setting the clending Color

> public function setBlendingColor(mixed $color): ImageInterface

Sets the blending color based on the specified color value. This can be
specified in one of the supported [color formats](/v3/introduction/formats#color-formats).

This color is only used if an output format is selected that does not support
an alpha channel and the transparency must therefore be replaced. **In other
cases, setting the color has no effect.** The default value is white.

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// read a PNG file with transparency
$image = $manager->read('images/example.png');

// define the replacement color for transparent areas
$image->setBlendingColor('#ff5500'); // orange

// encode file as jpeg
$image->toJpeg();
```

### Getting the Blending Color

> public function blendingColor(): ColorInterface

Reads out the current blending color of the image.

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// read an image
$image = $manager->read('images/example.png');

// read the replacement color for transparent areas
$color = $image->blendingColor(); // default white
```

### Merging Transparent Areas with Color

> public function blendTransparency(mixed $color = null): ColorInterface

When switching to a non-transparent image format, the transparency is
automatically replaced with the set blending color, but this can also be done
manually. This function call can also be applied to image formats that can
actually contain transparency.

The `color` parameter can optionally be used to specify a color in the common
[color formats](/v3/introduction/formats#color-formats). By default, this is
the current or previously set blending color.

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | mixed | Color to replace transparent areas (optional) |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// read a transparent image
$image = $manager->read('images/example.png');

// merge the transparent areas with orange
$image->blendTransparency('f50');
```
