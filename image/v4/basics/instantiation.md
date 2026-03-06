---
label: "Read & Create Images"
title: "Instantiation"
subtitle: "Read & Create Images"
lead: "Learn how to manage and process images with the Intervention Image Manager. Read and decode images from multiple sources like file paths, Base64, and Data Uri, or create custom images and animations using PHP."
sort: 1
---

[TOC]

## Read Images

### Read Image Sources

> public ImageManager::decode(mixed $source, null|string|array|DecoderInterface $decoders = null): ImageInterface

With a [configured Image Manager](/v4/basics/configuration-drivers) it is
possible to read images from different sources. The `decode()` method accepts
all available image sources. A complete list can be found below.

#### Parameters

| Name | Type | Description |
| - | - | - |
| source | mixed | Image source  |
| decoders | null, string, array or DecoderInterface | Decoder(s) to process the input data, by default decoders for all image sources are tried |

#### Supported Image Sources

The following `source` argument formats are accepted.

- Path in filesystem
- Raw binary image data
- `SplFileInfo` object
- Base64 encoded image data
- Data Uri string or instance of `DataUriInterface`
- Stream resource
- Instance of ImageInterface
- Instance of EncodedImageInterface

To decode the source, you can optionally specify a decoding strategy with the
second parameter. This can be an array of class names or objects of decoders to
be tried in sequence. It is also possible to pass a single object or class name
of a decoder. If the second parameter is not set, all available images decoders
will be tried.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read image from filesystem
$image = $manager->decode('images/example.jpg');

// read image from binary data
$image = $manager->decode(file_get_contents('images/example.jpg'));
```

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Decoders\DataUriImageDecoder;
use Intervention\Image\Decoders\Base64ImageDecoder;
use Intervention\Image\Decoders\FilePathImageDecoder;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read image only from data uri or base64 encoded data
$image = $manager->decode($input, [
    DataUriImageDecoder::class,
    Base64ImageDecoder::class,
]);

// read image only from file path
$image = $manager->decode($input, FilePathImageDecoder::class);

// same with object instead of class name
$image = $manager->decode($input, new FilePathImageDecoder());
```
### Read Images from File Paths

> public ImageManager::decodePath(string|Stringable $path): ImageInterface

Decode an image by using the given path in filesystem.

#### Parameters

| Name | Type | Description |
| - | - | - |
| path | string or Stringable | Image path  |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read image from filesystem
$image = $manager->decodePath('images/example.jpg');
```
### Read Images from Binary Data

> public ImageManager::decodeBinary(string|Stringable $binary): ImageInterface

Create an image instance by decoding the given raw binary image data.

#### Parameters

| Name | Type | Description |
| - | - | - |
| binary | string or Stringable | Binary image data  |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read image from binary
$image = $manager->decodeBinary(file_get_contents('images/example.jpg'));
```
### Read Images from SplFileInfo Objects

> public ImageManager::decodeSplFileInfo(SplFileInfo $splFileInfo): ImageInterface

Decode an image by decoding the image data of the given SplFileInfo instance.
This method can be used to handle image file uploads in the Laravel or Symfony
frameworks from `Illuminate\Http\UploadedFile` or `Symfony\Component\HttpFoundation\File\UploadedFile`.

#### Parameters

| Name | Type | Description |
| - | - | - |
| splFileInfo | SplFileInfo | Instance of SplFileInfo with image data |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read image from splFileInfo object
$image = $manager->decodeSplFileInfo(new SplFileInfo('example.jpg'));
```

### Read Images from Base64 Encoded Data

> public ImageManager::decodeBase64(string|Stringable $base64): ImageInterface

Create an image instance by decoding the given base64 encoded image data.

#### Parameters

| Name | Type | Description |
| - | - | - |
| base64 | string or Stringable | Base64 encoded image data |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read image from base64 encoded data
$image = $manager->decodeBase64('Zm9vYmFyYmF6MTIzNDU2Nzg5MA...');
```

### Read Images from Data Uri Scheme

> public ImageManager::decodeDataUri(string|Stringable|DataUriInterface $dataUri): ImageInterface

Create an image instance by decoding the image in the given data uri scheme.

#### Parameters

| Name | Type | Description |
| - | - | - |
| dataUri | string, Stringable or DataUriInterface | Image data encoded as data uri scheme.  |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read image from data uri
$image = $manager->decodeDataUri('data:image/jpeg,Zm9vYmFyYmF6MTIzNDU2Nzg5MA...');
```

### Read Images from Stream

> public ImageManager::decodeStream(mixed $stream): ImageInterface

Decode an image by using the given path in filesystem.

#### Parameters

| Name | Type | Description |
| - | - | - |
| stream | resource | Stream resource with image data |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// open new stream resource
$stream = fopen('example.jpg', 'r');

// read image from stream
$image = $manager->decodeStream($stream);
```

## Create Images

### Create New Images

> public function createImage(int $width, int $height, null|callable|AnimationFactoryInterface $animation = null): ImageInterface;

Reading existing image sources is one thing, but what if you want to create
your own images? Intervention Images can help you with that. You start with an
instance of the `Intervention\Image\ImageManager` class and call the
`createImage()` method with the desired image size as arguments. See the
following example:

By default the image is created with a **transparent background**. If you want to define a background color instead use the `fill()` method after creation.

Optionally you can pass a callback to add animation frames and create a
animated image and define the delay time of the individual animation frames. It
should be noted that the animation created this way must be decoded in a format
that supports animations.

Animations are possible in all supplied drivers. [Read more on how to modify animated images.](/v4/modifying-images/animations)

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Image width  |
| height | integer | Image height  |
| animation | null, callable or AnimationFactoryInterface | Optional callback for defining animation frames |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// create new image 640x480
$image = $manager->createImage(640, 480);

// create new image 512x512 with gray background
$image = $manager->createImage(512, 512)->fill('ccc');

// create new animated image 120x80 with five animation frames
$image = $manager->createImage(120, 80, function (AnimationFactoryInterface $animation): void {
    $animation->add('image.png', .25)->pixelate(20);
    $animation->add('image.png', .25)->pixelate(15);
    $animation->add('image.png', .25)->pixelate(10);
    $animation->add('image.png', .25)->pixelate(5);
    $animation->add('image.png', .25);
});
```
