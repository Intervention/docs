# Instantiation
## Reading & creating images

[TOC]

## Reading Images

### Reading image sources

> public ImageManager::make(mixed $source): ImageInterface

With Intervention Image you are able to read images from severeal different sources. The starting point is an instance of the `Intervention\Image\ImageManager` class. This class provides a universal method  `make()` to read different types of image sources.


#### Parameters

| Name | Type | Description |
| - | - | - |
| source | mixed | Image source  |

#### Supported image sources

This method not only supports filepaths as an argument. The following argument formats are accepted.

- Path in filesystem
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
$image = $manager->make('images/example.jpg');

// read image from binary data
$image = $manager->make(file_get_contents('images/example.jpg'));
```

## Creating Images

### Creating new images

> public ImageManager::create(int $width, int $height, mixed $background = 'transparent'): ImageInterface

Reading existing image sources is one thing, but what if you want to create your own images? Intervention Images can help you with that. You start with an instance of the `Intervention\Image\ImageManager` class and call the `create()` method with the desired image size as arguments. See the following example:

By default the image is created with a **transparent background**. If you want to define a background color instead use an optional third parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Image width  |
| height | integer | Image height  |
| background (optional) | mixed | Background color  |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// create new image 640x480
$image = $manager->create(640, 480);

// create new image 512x512 with grey background
$image = $manager->create(512, 512, 'ccc');
```