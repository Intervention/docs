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
$manager = new ImageManager('gd');

// true
$result = $manager->read('images/animation.gif')->isAnimated();
```

## Editing animations

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
$manager = new ImageManager('gd');

// reading an animated gif
$image = $manager->read('images/animation.gif');

// animation should only run once
$image = $image->setLoops(1);
```

### Removing animation

> public Image::removeAnimation(int $position = 0): ImageInterface

Discards all animation frames of the current image instance except the one at the given position. Turns an animated image into a static one.

#### Parameters

| Name | Type | Description |
| - | - | - |
| position | integer | Position of the frame that will be left |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an animated gif
$image = $manager->read('images/animation.gif');

// Turn the animation into a static image displaying the frame at position 5
$image = $image->removeAnimation(5);
```

