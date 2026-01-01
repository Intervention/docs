---
title: "Image Effects"
subtitle: "Apply Image Effects"
lead: "Learn how to apply various image effects using the Intervention Image library. Adjust brightness, contrast, and colors, convert to greyscale, add gamma correction, mirror, rotate, blur, sharpen, invert colors, pixelate, and reduce colors."
sort: 2
---

[TOC]

## Brightness, Contrast & Colors

### Change the Image Brightness

> public Image::brightness(int $level): ImageInterface

Change the brightness of the current image by a given level. Use values between `-100` for minimum brightness `0` for no change and `+100` for maximum brightness.

#### Parameters

| Name | Type | Description |
| - | - | - |
| level | integer | Level of brightness change  |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an image
$image = $manager->read('images/example.png');

// increase brightness
$image = $image->brightness(35);
```


### Change the Image Contrast

> public Image::contrast(int $level): ImageInterface

Change the contrast of the current image by a given level. Use values between `-100` for minimum contrast `0` for no change and `+100` for maximum contrast.

#### Parameters

| Name | Type | Description |
| - | - | - |
| level | integer | Level of contrast change  |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// read an image
$image = $manager->read('images/example.png');

// decrease the contrast
$image = $image->contrast(-10);
```

### Gamma Correction

> public Image::gamma(float $gamma): ImageInterface

Apply a gamma correction operation to the current image.

#### Parameters

| Name | Type | Description |
| - | - | - |
| gamma | float | Gamma compensation value |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::gd();

// read an image
$image = $manager->read('images/example.jpg');

// apply gamma correction
$image = $image->gamma(1.7);
```

### Color Correction

> public Image::colorize(int $red = 0, int $green = 0, int $blue = 0): ImageInterface

Change the intensity level of the given red, green and blue color values.
The input values are normalized so you need to include parameters from `100` for
maximum color intensity to `0` for no change and `-100` to remove all the specific
color from the image.

#### Parameters

| Name | Type | Description |
| - | - | - |
| red | int | Intensity correction of all red colors in image |
| green | int | Intensity correction of all green colors in image |
| blue | int | Intensity correction of all blue colors in image |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = ImageManager::withDriver(Driver::class);

// read an image
$image = $manager->read('images/example.jpg');

// change colors to a blue & green tone
$image = $image->colorize(blue: 15, green: 10);
```

### Convert image to a greyscale version

> public Image::greyscale(): ImageInterface

Converts the current image to a greyscale version.

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// read a colored image
$image = $manager->read('images/example.jpg');

// turn image into a greyscale version
$image = $image->greyscale();
```





## Various Effects

### Mirror Image Horizontally

> public Image::flop(): ImageInterface

Mirror the current image horizontally by swapping left and right.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an image
$image = $manager->read('images/example.png');

// mirror image horizontally
$image = $image->flop();
```

### Mirror Image Vertically

> public Image::flip(): ImageInterface

Mirror the current image vertically by swapping top and bottom.

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// read an image
$image = $manager->read('images/example.png');

// mirror image vertically
$image = $image->flip();
```

### Image Rotation

> public Image::rotate(float $angle, mixed $background = 'ffffff'): ImageInterface

Rotate the current image counterclockwise by the specified angle. Optionally,
specify a background color to fill the newly created uncovered areas after the
rotation.

#### Parameters

| Name | Type | Description |
| - | - | - |
| angle | float | The rotation angle in degrees to rotate the image counterclockwise |
| background | mixed | A color to fill the newly created areas after rotation |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::gd();

// read an image
$image = $manager->read('images/example.png');

// rotate image 45 degrees clockwise 
$image = $image->rotate(-45);
```



### Image Orientation According to Exif Data

> public Image::orient(): ImageInterface

This method uses Exif data to automatically orient images correctly. **This
rotation is done automatically by default.** So you don't need to call this
method unless you have [disabled the auto orientation in the ImageManager
configuration](/v3/basics/configuration-drivers).

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance without auto exif orientation
$manager = ImageManager::gd(autoOrientation: false);

// read the image
$image = $manager->read('images/example.jpg');

// orient image according to exif data
$image = $image->orient();
```








### Blur Effect

> public Image::blur(int $amount = 5): ImageInterface

Applies a gaussian blur effect to the current image. Use the optional `amount` argument to specify the strength of the effect with values between `0` and `100`.

**With the GD driver this method is performance intensive for larger blur amounts. Use with caution.**

#### Parameters

| Name | Type | Description |
| - | - | - |
| amount | integer | Effect strength value (0 - 100)  |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading an image
$image = $manager->read('images/example.png');

// apply blurring effect
$image = $image->blur(3);
```


### Sharpening Effect

> public Image::sharpen(int $amount = 10): ImageInterface

Sharpen the current image instance by an optional `amount`.

#### Parameters

| Name | Type | Description |
| - | - | - |
| amount | integer | The amount of the sharpening strength. (0 - 100)  |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// reading an image
$image = $manager->read('images/example.png');

// apply sharpening effect
$image = $image->sharpen(3);
```


### Invert Colors

> public Image::invert(): ImageInterface

Invert all colors in the current image.

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::gd();

// reading an image
$image = $manager->read('images/example.png');

// invert colors
$image = $image->invert();
```


### Pixelation Effect

> public Image::pixelate(int $size): ImageInterface

Applies a pixelation effect to the current image with a given pixel size.

#### Parameters

| Name | Type | Description |
| - | - | - |
| size | integer | Size of the pixels. |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::withDriver(new Driver());

// reading an image
$image = $manager->read('images/example.png');

// apply the pixelation effect
$image = $image->pixelate(12);
```

### Reduce Colors

> public Image::reduceColors(int $limit, mixed $background = 'transparent'): ImageInterface

Apply color quantization to the current image by reducing the number of
distinct colors in the current image to the given limit. The number of colors
is reduced in a way that the new image is as visually similar as possible.

With the GD driver (semi-)transparent colors that lose their transparency as a
result of the reduction process are blended against the given background color.

#### Parameters

| Name | Type | Description |
| - | - | - |
| limit | integer | Allowed number of distinct colors |
| mixed | background | Color formerly semi-transparent colors are blended against |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// reading an image
$image = $manager->read('images/example.png');

// quantize colors to a maximum of 16
$image = $image->reduceColors(16);
```
