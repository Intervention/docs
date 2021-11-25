# Image Effects
## Applying image effects

[TOC]

## Brightness & Contrast

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

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->make('images/example.png');

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

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->make('images/example.png');

// decreasing the contrast
$image = $image->contrast(-10);
```

## Various Effects

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

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->make('images/example.png');

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
$manager = new ImageManager('gd');

// reading an image
$image = $manager->make('images/example.png');

// apply blurring effect
$image = $image->blur(3);
```


### Invert colors

> public Image::invert(): ImageInterface

Invert all colors of the current image.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->make('images/example.png');

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
$manager = new ImageManager('gd');

// reading an image
$image = $manager->make('images/example.png');

// apply the pixelation effect
$image = $image->pixelate(12);
```
