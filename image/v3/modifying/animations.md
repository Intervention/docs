# Animations
## Changing details of animated images

[TOC]

## Detect animations

### Check the current image instance for animation

> public Image::isAnimated(): bool

Returns `true` if the image is animated. Otherwise `false` is returned.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// true
$result = $manager->read('images/animation.gif')->isAnimated();
```

## Editing animations

### Reading the Animation Iteration Count

> public Image::loops(): int

Read the count of iterations of the animated image. `0` means the image loops continuously.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

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

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading an animated gif
$image = $manager->read('images/animation.gif');

// animation should only run once
$image = $image->setLoops(1);
```

### Removing animation

> public Image::removeAnimation(int|string $position = 0): ImageInterface

Discards all animation frames of the current image instance except the one at
the given position. Turns an animated image into a static one.

It is possible to specify the position as integer and string values. With the
former, the exact position passed is searched for, while string values must
represent a percentage value and the respective frame position is only
determined approximately.

If an integer is specified, the method throws an exception if the respective
position is not found. This does not happen with percentage values.

#### Parameters

| Name | Type | Description |
| - | - | - |
| position | integer or string | Position of the frame that will be left. |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading an animated gif
$image = $manager->read('images/animation.gif');

// Turn the animation into a static image displaying the frame at position 5
$image = $image->removeAnimation(5);
```

## Animation Frames
### Read Animation Frames

> public Image::frame(int $position = 0): FrameInterface

Read the animation frame at the given position.

#### Parameters

| Name | Type | Description |
| - | - | - |
| position | integer | Position of the retrieved frame |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading an animated gif
$image = $manager->read('images/animation.gif');

// Read frame 15
$frame = $image->frame(15);

// turn frame into image for further processing
$frame_image = $frame->toImage();
```
