# Animations
## Creating & editing animated images

### Creating Animations

> public ImageManager::animate(int $width, int $height, callable $callback): ImageInterface

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// create an animated image
$image = $manager->animate(300, 200, function ($animation) {
    $animation->addFrame('images/frame_01.png', 125);
    $animation->addFrame('images/frame_02.png', 125);
    $animation->addFrame('images/frame_03.png', 125);
    $animation->loops(12);
});

// save as animated gif
$image->toGif()->save('/images/animation.gif')
```

### Discard animations

> public Image::discardAnimation(int $frame = 0): ImageInterface

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// read animation
$image = $manager->make('images/animation.gif');

// discard animation except second frame
$image->discardAnimation(2);
```
