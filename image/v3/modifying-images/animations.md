---
title: "Animations"
subtitle: "Change Details of Animated Images"
lead: "Master image animation handling with Intervention Image. Learn to edit and customize animated images like GIF format, including frame slicing, iteration control, and converting animations to static images."
sort: 5
---

[TOC]

Both drivers included with Intervention Image support animation by default.
However, the GD driver must use additional resources as it does not support
animation out of the box.

If you are loading images without the intention of processing the animation at
all, this process can be [disabled beforehand in the Image
Manager](/v3/basics/configuration-drivers) configuration to save resources.

## Create Animations

More information about the animation creation process can be found in the chapter about [instantiation](/v3/basics/instantiation#create-animations).

## Detect Animations
### Check the Current Image Instance for Animation

> public Image::isAnimated(): bool

Returns `true` if the image is animated. Otherwise `false`.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// true
$result = $manager->read('images/animation.gif')->isAnimated();
```

## Edit Animations

### Read the Animation Frame Count

> public Image::count(): int

Read the number of animation frames. `ImageInterface::class` extends
`Countable::class`, so it is also possible to use the image object with the
[count()](https://www.php.net/manual/en/function.count.php) function.

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::gd();

// read an animated gif
$image = $manager->read('images/animation.gif');

// read number if animation frames
$count = $image->count();

// same result with count() function
$count = count($image);
```

### Change the Animation Frames

> public Image::sliceAnimation(int $offset, null|int $length = null): ImageInterface

Extract animation frames based on given values and discard the rest. The offset
parameter can be used to set the starting point of the new animation; all
frames before the offset will be discarded. The length parameter is optional.
It specifies how many frames to read after the offset. The default is to read
all frames up to the end of the animation.

#### Parameters

| Name | Type | Description |
| - | - | - |
| offset | integer | Starting point of the new animation |
| length | null or integer | Frames to read after the offset (optional) |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an animated gif
$image = $manager->read('images/animation.gif');

// discard the first 20 frames and read the following 10 frames as new animation
$image = $image->sliceAnimation(20, 10);
```

### Read the Animation Iteration Count

> public Image::loops(): int

Read the count of iterations of the animated image. `0` means the image loops continuously.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an animated gif
$image = $manager->read('images/animation.gif');

// return animation iteration count
$count = $image->loops();
```

### Change the Animation Iteration Count

> public Image::setLoops(int $count): ImageInterface

Change the number of iterations the animation should loop over. Set to `0` to loop continuously.

#### Parameters

| Name | Type | Description |
| - | - | - |
| count | integer | Number of animation iterations |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an animated gif
$image = $manager->read('images/animation.gif');

// animation should only run once
$image = $image->setLoops(1);
```

### Remove Animation

> public Image::removeAnimation(int|string $position = 0): ImageInterface

Turns an animated image into a non-animated one by discarding all animation
frames of the current image instance except the one at the given position. 

The position can be specified as an integer or string value. With
integer, the exact frame number starting from 0 is used as the remaining frame.
String values must be a percentage value between `0%` and `100%`
and the remaining frame number is only determined approximately.

If the position is specified as an integer, the method throws an exception if
the frame doesn't exist. This is not the case with percentage values, as a
frame can always be found.

#### Parameters

| Name | Type | Description |
| - | - | - |
| position | integer or string | Position of the frame that will be left. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// read an animated gif
$image = $manager->read('images/animation.gif');

// Turn the animation into a static image displaying the frame at position 5
$image = $image->removeAnimation(5);

// do the same by choosing animation frame at 25% of the whole animation
$image = $image->removeAnimation('25%');

```
