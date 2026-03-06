---
label: "Image Output"
title: "Image Output"
subtitle: "Encode Images in Different Formats"
lead: "Learn how to encode images with Intervention Image, including support for various formats like JPEG, PNG, WebP, and AVIF. Discover versatile methods to encode by file path, media type, or file extension, with customization options."
sort: 5
---

[TOC]

## Save Images to File System

### Encode & Save Combined

> public Image::save(null|string $path = null, mixed ...$options): ImageInterface

This method helps to initiate the saving process directly from the image object
without having to go via an `EncodedImage` object and encodes & writes the
image data in one call.

The resulting image format is defined by the file extension of the given path. For example if you pass `images/test.jpg` the image format will be JPEG, if `images/test.gif` is passed the format will be GIF. If no path is given the format of the originally read image will be used. 

After the path you can pass encoder options like `quality`, `strip` or `interlaced` - these depend on the recognized format.

The encoded image is saved at the given path in the local file system. The folder structure must already exist and be writable.

In contrast to the other encoding methods, `save()` returns an `Image` object instead of an `EncodedImage` object.

#### Parameters

| Name | Type | Description |
| - | - | - |
| path (optional) | null or string | File path from which the target format is extracted. By default the original path is used. |
| options (optional) | mixed | Option encoder parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read jpeg image
$image = $manager->decode('images/example.jpg');

// overwrite file at "images/example.jpg" with low quality
$image->save(quality: 10);

// encode original jpeg format as png and save in a new file
$image->save('images/example.png');

// encode & save progressive jpeg in low quality
$image->save('images/example.jpg', quality: 10, progressive: true);
```

## Encode Images

### Encode Images using Format

> public Image::encodeUsingFormat(Format $format, mixed ...$options): EncodedImageInterface

Encode the current image using the given `Intervention\Image\Format` enum value to resolve an
encoder. Define optional encoder options with additional parameters.

#### Parameters

| Name | Type | Description |
| - | - | - |
| format | `Intervention\Image\Format` | Format enum value to set the target format |
| options (optional) | mixed | Option parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Format;

// create new manager instance and read image
$image = ImageManager::usingDriver(Driver::class)->decode('example.webp');

// encode to PNG format
$png = $image->encodeUsingFormat(Format::PNG);

// encode in JPEG format with encoder options
$jpeg = $image->encodeUsingFormat(Format::JPEG, progressive: true, quality: 10);

// encode to GIF format
$gif = $image->encodeUsingFormat(Format::GIF);
```


### Encode Images using Media (MIME) Types

> public Image::encodeUsingMediaType(string|MediaType $mediaType, mixed ...$options): EncodedImageInterface

Encode the current image using a given media (mime) type to determine the
encoder. The media type can be passed as string or
`Intervention\Image\MediaType` enum value. Define optional encoder options with
additional parameters.

#### Parameters

| Name | Type | Description |
| - | - | - |
| mediaType | string or `Intervention\Image\MediaType` | Media (MIME) type to define the encoding target format. |
| options (optional) | mixed | Option parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\MediaType;

// create new manager instance and read image
$image = ImageManager::usingDriver(Driver::class)->decode('example.webp');

// encode to PNG format
$png = $image->encodeUsingMediaType(MediaType::IMAGE_PNG);

// encode in JPEG format with encoder options
$jpeg = $image->encodeUsingMediaType(MediaType::IMAGE_JPEG, progressive: true, quality: 10);

// encode to GIF format by using string mime type
$gif = $image->encodeUsingMediaType('image/gif');
```

### Encode Images using File Extensions

> public Image::encodeUsingFileExtension(string|FileExtension $fileExtension, mixed ...$options): EncodedImageInterface

Encode the current image using a file extension string or enum value to determine the
encoder. The file extension can be passed as string or `Intervention\Image\FileExtension` enum value. 
Set optional encoder options with additional parameters.

#### Parameters

| Name | Type | Description |
| - | - | - |
| fileExtension | string or `Intervention\Image\FileExtension` | File extension to set the image format of the encoder |
| options (optional) | mixed | Option parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\FileExtension;

// create new manager instance and read image
$image = ImageManager::usingDriver(Driver::class)->decode('example.webp');

// encode to PNG format
$png = $image->encodeUsingFileExtension(FileExtension::PNG);

// encode in JPEG format with encoder options
$jpeg = $image->encodeUsingFileExtension(FileExtension::JPG, progressive: true, quality: 10);

// encode to Webp format using string file extension
$gif = $image->encodeUsingFileExtension('webp', quality: 10);
```

### Encode Images using File Paths

> public Image::encodeUsingPath(string $path, mixed ...$options): EncodedImageInterface

Encode the current image using a file path or file name to determine the encoder by
the file extension. Set optional encoder options with additional parameters.

It is important to note that the given file path or name is not written. It is
only used to determine the encoder format. Use [save()](/) if you want to write.

#### Parameters

| Name | Type | Description |
| - | - | - |
| path | string | File path to determine the image format from the file extension |
| options (optional) | mixed | Option parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance and read image
$image = ImageManager::usingDriver(Driver::class)->decode('example.webp');

// encode to PNG format
$png = $image->encodeUsingFilePath('images/output.png');

// encode in JPEG format with encoder options
$jpeg = $image->encodeUsingFilePath('images/output.jpg', progressive: true, quality: 10);

// encode to Webp format using file extension of a file name
$gif = $image->encodeUsingFilePath('output.webp', quality: 10);
```


### Encode Images with Encoder Objects

> public Image::encode(null|string|EncoderInterface $encoder = new AutoEncoder()): EncodedImage

This method encodes the image with the given encoder object. The following encoders
are currently available.

- `Intervention\Image\Encoders\AutoEncoder::class`
- `Intervention\Image\Encoders\JpegEncoder::class`
- `Intervention\Image\Encoders\WebpEncoder::class`
- `Intervention\Image\Encoders\PngEncoder::class`
- `Intervention\Image\Encoders\GifEncoder::class`
- `Intervention\Image\Encoders\AvifEncoder::class`
- `Intervention\Image\Encoders\BmpEncoder::class`
- `Intervention\Image\Encoders\TiffEncoder::class`
- `Intervention\Image\Encoders\Jpeg2000Encoder::class`
- `Intervention\Image\Encoders\HeicEncoder::class`
- `Intervention\Image\Encoders\IcoEncoder::class`

If no encoder is passed the `AutoEncoder` is used which will attempt to detect
the output format automatically according to the original format of the image.

#### Parameters

| Name | Type | Description |
| - | - | - |
| encoder (optional) | EncoderInterface | Image encoder with which the image is transformed |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Encoders\AutoEncoder;
use Intervention\Image\Encoders\WebpEncoder;
use Intervention\Image\Encoders\GifEncoder;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read jpeg image
$image = $manager->decode('images/example.jpg');

// encode as the originally read image format
$encoded = $image->encode(); // Intervention\Image\EncodedImage

// encode as the originally read image format but with a certain quality
$encoded = $image->encode(new AutoEncoder(quality: 10)); // Intervention\Image\EncodedImage

// encode jpeg as webp format
$encoded = $image->encode(new WebpEncoder(quality: 65)); // Intervention\Image\EncodedImage

// result will be gif format
$encoded = $image->encode(new GifEncoder()); // Intervention\Image\EncodedImage
```

## Handling of Encoded Image Data

The mentioned encoding methods return an `Intervention\Image\EncodedImage`
object. With this instance you can decide how to proceed with the encoded data.

### Cast Encoded Image Data to String

> public EncodedImage::__toString(): string

This method can be used to obtain the raw image data as type string. This is
particularly useful if it is to be further processed with other libraries or
transferred to remote cloud storage for example.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Format;
use Example\CloudStorage;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// resize gif image
$image = $manager
    ->decode('images/example.gif')
    ->scale(height: 200);

// encode in jpeg format and cast result as string
$imagedata = (string) $image->encodeUsingFormat(Format::JPEG);

// save to data service
CloudStorage::put('example.jpg', $imagedata);
```



### Save Encoded Image Data in Filesystem

> public EncodedImage::save(string $path): void

This method writes the object's data to the given path in the local file system. The
respective folder structure must already exist and be writable.

#### Parameters

| Name | Type | Description |
| - | - | - |
| filepath | string | Path to file in filesystem. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Format;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// reading gif image
$image = $manager->decode('images/example.gif');

// save progressive jpeg file in low quality
$encoded = $image->encodeUsingFormat(Format::JPEG, progressive: true, quality: 25)->save('images/test.jpg');
```


### Create Data URI Scheme

> public EncodedImage::toDataUri(): string

This method takes the already encoded image data and wraps it in an base64 encoded data uri scheme. 

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read gif image
$image = $manager->decode('images/example.gif');

// encode to original format (gif) and transform to data uri
$dataUri = $image->encode()->toDataUri();
```

### Transform Encoded Image to File Pointer

> public EncodedImage::toFilePointer(): resource

Create a file pointer resource to handle the encoded image data.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Format;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read gif image
$image = $manager->decode('images/example.gif');

// create file pointer
$pointer = $image->encodeUsingFormat(Format::JPEG)->toFilePointer();
```

### Retrieve Media (MIME) Type of an Encoded Image

> public EncodedImage::mediaType(): string

This method returns the media (MIME) type of the encoded image.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read gif image
$image = $manager->decode('images/example.gif');

// "image/jpeg"
$mimetype = $image->encodeUsingFileExtension(FileExtension::JPG)->mediaType();
```


