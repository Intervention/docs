# Image Effects
## Applying Image Effects

[TOC]

## Brightness, Contrast & Colors

### Changing the Brightness

> public Image::brightness(int $level): ImageInterface

Change the brightness of the current image by a given level. Use values between `-100` for min. brightness `0` for no change and `+100` for max. brightness.

#### Parameters

| Name | Type | Description |
| - | - | - |
| level | integer | Level of brightness change  |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an image
$image = $manager->read('images/example.png');

// increase brightness
$image = $image->brightness(35);
```


### Changing the Contrast

> public Image::contrast(int $level): ImageInterface

Change the contrast of the current image by a given level. Use values between `-100` for min. contrast `0` for no change and `+100` for max. contrast.

#### Parameters

| Name | Type | Description |
| - | - | - |
| level | integer | Level of contrast change  |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading an image
$image = $manager->read('images/example.png');

// decreasing the contrast
$image = $image->contrast(-10);
```

### Gamma Correction

> public Image::gamma(float $gamma): ImageInterface

Apply a gamma correction operation on the current image.

#### Parameters

| Name | Type | Description |
| - | - | - |
| gamma | float | Gamma compensation value |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::gd();

// reading an image
$image = $manager->read('images/example.jpg');

// apply gamma correction
$image = $image->gamma(1.7);
```

### Color Correction

> public Image::colorize(int $red = 0, int $green = 0, int $blue = 0): ImageInterface

Change the intensity level of the given color values of red, green and blue.
The input values are normalized so you have to include parameters from 100 for
maximum color intesity to 0 for no change and -100 to remove all the certain
color on the image.

#### Parameters

| Name | Type | Description |
| - | - | - |
| red | int | Intesity correction of all red colors in image |
| green | int | Intesity correction of all green colors in image |
| blue | int | Intesity correction of all blue colors in image |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = ImageManager::withDriver(Driver::class);

// reading an image
$image = $manager->read('images/example.jpg');

// change colors to a blue & green tone
$image = $image->gamma(blue: 15, green: 10);
```

### Convert image to a grayscale version

> public Image::greyscale(): ImageInterface

Converts the current image into a grayscale version.

#### Examples

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

Mirror the current image horizontally.

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an image
$image = $manager->read('images/example.png');

// mirror image
$image = $image->flop();
```


### Mirror Image Vertically

> public Image::flip(): ImageInterface

Mirror the current image vertically.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// reading an image
$image = $manager->read('images/example.png');

// flood fill image with color
$image = $image->flip();
```

### Image Rotation

> public Image::rotate(float $angle, mixed $background = 'ffffff'): ImageInterface

Rotates the current image counterclockwise by the specified angle. Optionally,
specify a background color to fill the newly created uncovered areas after the
rotation.

#### Parameters

| Name | Type | Description |
| - | - | - |
| angle | float | The rotation angle in degrees to rotate the image counterclockwise |
| background | mixed | A color to fill the newly created areas after rotation |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::gd();

// reading an image
$image = $manager->read('images/example.png');

// rotate image 45 degrees clockwise 
$image = $image->rotate(-45);
```

### Blur Effect

> public Image::blur(int $amount = 5): ImageInterface

Apply a gaussian blur effect on the current image. Use the optional `amount` argument to define the effect strenght with values between `0` and `100`.

**With GD driver this method is performance intensive on larger amounts of blur. Use with care.**

#### Parameters

| Name | Type | Description |
| - | - | - |
| amount | integer | Effect strength value (0 - 100)  |

#### Examples

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

Sharpen the current image instance with an optional `amount`.

#### Parameters

| Name | Type | Description |
| - | - | - |
| amount | integer | The amount of the sharpening strength. (0 - 100)  |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// reading an image
$image = $manager->read('images/example.png');

// apply blurring effect
$image = $image->blur(3);
```


### Invert Colors

> public Image::invert(): ImageInterface

Invert all colors of the current image.

#### Examples

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

Applies a pixelation effect on the current image with a given pixel size.

#### Parameters

| Name | Type | Description |
| - | - | - |
| size | integer | Size of the pixels. |

#### Examples

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

Apply color quantization to the current image by reducing the numbers of
distinct colors in the current image to the given limit. The number of colors
is lowered in a way that the new image should be as visually similar as
possible.

With GD driver (semi-)transparent colors that lose their transparency as a
result of the reduction process are blended against the given background color.

#### Parameters

| Name | Type | Description |
| - | - | - |
| limit | integer | Allowed number of distinct colors |
| mixed | background | Color formerly semi-transparent colors are blended against |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// reading an image
$image = $manager->read('images/example.png');

// quantize colors to a maximum of 16
$image = $image->reduceColors(16);
```
