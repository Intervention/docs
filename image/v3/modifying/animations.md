# Animations
## Change Details of Animated Images
Master image animation handling with Intervention Image. Learn to edit and customize animated images like GIF format, including frame slicing, iteration control, and converting animations to static images.

[TOC]

By default, both drivers included with Intervention Image support animations.
However, the GD driver must use additional resources as it does not has
animation support by default. 

If you read images without the intention of processing the animation at all,
this process can be [deactivated in advance in the image manager
configuration](/v3/basics/image-manager) to save resources.

## Detect Animations
### Check the Current Image Instance for Animation

> public Image::isAnimated(): bool

Returns `true` if the image is animated. Otherwise `false` is returned.

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// true
$result = $manager->read('images/animation.gif')->isAnimated();
```

## Editing Animations

### Reading the Animation Frame Count

> public Image::count(): int

Read the number of animation frames. `ImageInterface::class` extends
`Countable::class`, so it is possible to use the image object with the
[count()](https://www.php.net/manual/en/function.count.php) function.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::gd();

// reading an animated gif
$image = $manager->read('images/animation.gif');

// read number if animation frames
$count = $image->count();

// same result with count() function
$count = count($image);
```

### Changing the Animation Frames

> public Image::sliceAnimation(int $offset, null|int $length = null): ImageInterface

Extract animation frames based on given values and discard the rest. The offset
parameter can be used to set the starting point of the new animation; all
frames before the offset are discarded. The length parameter is optional. It
specifies how many frames to read after the offset. By default, all frames up
to the end of the animation are read.

#### Parameters

| Name | Type | Description |
| - | - | - |
| offset | integer | Starting point of the new animation |
| length | null or integer | Frames to read after the offset (optional) |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an animated gif
$image = $manager->read('images/animation.gif');

// discard the first 20 frames and read the following 10 frames as new animation
$image = $image->sliceAnimation(20, 10);
```

### Reading the Animation Iteration Count

> public Image::loops(): int

Read the count of iterations of the animated image. `0` means the image loops continuously.

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an animated gif
$image = $manager->read('images/animation.gif');

// return animation iteration count
$count = $image->loops();
```

### Changing the Animation Iteration Count

> public Image::setLoops(int $count): ImageInterface

Change the number of iterations the animation should loop over. Set to `0` to loop continuously.

#### Parameters

| Name | Type | Description |
| - | - | - |
| count | integer | Number of animation iterations |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an animated gif
$image = $manager->read('images/animation.gif');

// animation should only run once
$image = $image->setLoops(1);
```

### Removing Animation

> public Image::removeAnimation(int|string $position = 0): ImageInterface

Discards all animation frames of the current image instance except the one at
the given position. Turns an animated image into a static one.

It is possible to specify the position as integer and string values. With the
former, the exact position passed is searched for, while string values must
represent a percentage value between `0%` and `100%` and the respective frame
position is only determined approximately.

If an integer is specified, the method throws an exception if the respective
position is not found. This does not happen with percentage values.

#### Parameters

| Name | Type | Description |
| - | - | - |
| position | integer or string | Position of the frame that will be left. |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading an animated gif
$image = $manager->read('images/animation.gif');

// Turn the animation into a static image displaying the frame at position 5
$image = $image->removeAnimation(5);

// do the same by choosing animation frame at 25% of the whole animation
$image = $image->removeAnimation('25%');

```
