# Instantiation
## Reading & creating images

[TOC]

## Reading Images

### Reading image sources

> public ImageManager::read(mixed $source): ImageInterface

With Intervention Image you are able to read images from severeal different
sources. The starting point is an instance of the
`Intervention\Image\ImageManager` class. This class provides a universal method
`read()` to read different types of image sources.

#### Parameters

| Name | Type | Description |
| - | - | - |
| source | mixed | Image source  |

#### Supported image sources

This method not only supports filepaths as an argument. The following argument formats are accepted.

- Path in filesystem
- File Pointer resource
- Raw binary image data
- Base64 encoded image data
- Data Uri
- Intervention Image Instance

If the given argument can not be decoded by the library an exception of type `Intervention\Image\Exceptions\DecoderException` is thrown.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('imagick');

// read image from filesystem
$image = $manager->read('images/example.jpg');

// read image from binary data
$image = $manager->read(file_get_contents('images/example.jpg'));
```

## Creating Images

### Creating new images

> public ImageManager::create(int $width, int $height): ImageInterface

Reading existing image sources is one thing, but what if you want to create your own images? Intervention Images can help you with that. You start with an instance of the `Intervention\Image\ImageManager` class and call the `create()` method with the desired image size as arguments. See the following example:

By default the image is created with a **transparent background**. If you want to define a background color instead use the `fill()` method after creation.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Image width  |
| height | integer | Image height  |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// create new image 640x480
$image = $manager->create(640, 480);

// create new image 512x512 with grey background
$image = $manager->create(512, 512)->fill('ccc');
```

### Creating animations

> public ImageManager::animate(callable $callback): ImageInterface

It is also possible to create animated graphics. To do this, use the "animate"
function. A callback function is passed to this function, which determines the
source and the delay time of the individual animation images. It should be
noted that the animation created in this way is output in a format that
supports animations at all.

Animations are possible in all supplied drivers. [Read more on how to modify animated images.](/v3/modifying/animations)

#### Parameters

| Name | Type | Description |
| - | - | - |
| callback | callable | Animation setup |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// create animated image with three frames and a delay of 250 ms for each frame
$image = $manager->animate(function ($animation) use ($manager) {
    $animation->add('images/frame01.png', .25);
    $animation->add('images/frame02.png', .25);
    $animation->add('images/frame03.png', .25);
})->setLoops(4);
```
