# Image Output
## Encoding images in different formats

[TOC]

## Encoding Images

### Encode Images with Encoder Objects

> public Image::encode(EncoderInterface $encoder = new AutoEncoder()): EncodedImage

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
$manager = new ImageManager(Driver::class);

// reading jpeg image
$image = $manager->read('images/example.jpg');

// encode as the originally read image format
$encoded = $image->encode(); // Intervention\Image\EncodedImage

// encode as the originally read image format but with a certain quality
$encoded = $image->encode(new AutoEncoder(quality: 10)); // Intervention\Image\EncodedImage

// encode jpeg as webp format
$encoded = $image->encode(new WebpEncoder(quality: 65)); // Intervention\Image\EncodedImage

// result will be gif format
$encoded = $image->encode(new GifEncoder()); // Intervention\Image\EncodedImage
```




### Encode Images by Media (MIME) Type

> public Image::encodeByMediaType(?string $type = null, mixed ...$options): EncodedImage

Encode an image to given media (mime) type. 

If no media type is given the image will be encoded to the format of the
originally read image's mime type.

#### Parameters

| Name | Type | Description |
| - | - | - |
| type (optional) | null or string | Target media (MIME) type into which the image is encoded. By default the original media type is used. |
| options (optional) | mixed | Option parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\MediaType;

// create new manager instance and read webp image
$image = new ImageManager(Driver::class)
    ->read('images/example.webp');

// encoded result will be the same as original
$encoded = $image->encodeByMediaType();

// encoded result will be the same as original but with low quality
$encoded = $image->encodeByMediaType(quality: 10);

// encoded result will be in progressive jpeg format
$encoded = $image->encodeByMediaType('image/jpeg', progressive: true, quality: 20);

// result will be in gif format
$encoded = $image->encodeByMediaType('image/gif');

// or use member of MediaType enum
$encoded = $image->encodeByMediaType(MediaType::IMAGE_GIF);
```










### Encode Images by File Path

> public Image::encodeByPath(?string $path = null, mixed ...$options): EncodedImage

Encode the image into the format represented by the extension of the given file
path. Add an optional second value to set the resulting image quality. If no
path is given the image will be encoded to the format of the originally read
image.

**Note that this method does not write the given path, but only uses this
information to extract the target format.**

#### Parameters

| Name | Type | Description |
| - | - | - |
| path (optional) | null or string | File path from which the target format is extracted. By default the original file path is used. |
| options (optional) | mixed | Option parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;

// image file path
$path = 'images/example.png';

// create new manager instance and read from path
$image = new ImageManager::imagick() ->read($path);

// encoded format will be the same as original
$encoded = $image->encodeByPath();

// resulting format will be the same as original but with low quality
$encoded = $image->encodeByPath(quality: 10);

// resulting format will jpeg because "jpg" represents jpeg format
$encoded = $image->encodeByPath('images/example.jpg', progressive: true, quality: 10);

// result will be gif format
$encoded = $image->encodeByPath('images/example.gif');
```







### Encode Images by File Extension

> public Image::encodeByExtension(?string $extension = null, mixed ...$options): EncodedImage

Encode the image into the format represented by the given file extension.
Define the image quality with the optional second parameter. If no extension is
given the image will be encoded to the format of the originally read image.

#### Parameters

| Name | Type | Description |
| - | - | - |
| extension (optional) | null, string, FileExtension | File extension that determines the target format. By default the original file extension is used. |
| options (optional) | mixed | Option parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance and read image
$image = new ImageManager::gd() ->read('example.jpg');

// resulting format will be the same as original
$encoded = $image->encodeByExtension();

// resulting format will be the same as original but with low quality
$encoded = $image->encodeByExtension(quality: 10);

// result will be jpeg format
$encoded = $image->encodeByExtension('jpg', progressive: true, quality: 10);

// result will be PNG format
$encoded = $image->encodeByExtension('png');

// alternatively use member of FileExtension enum
$encoded = $image->encodeByExtension(FileExtension::PNG);
```







## Encoding with Shortcut Methods

There is a corresponding shortcut method for each image format, which can be
called up directly from the image object.

### Encoding JPEG Format

> public Image::toJpeg(int $quality = 75, bool $progressive = false): EncodedImage

Encode the current image instance in JPEG format in the given **quality**
ranging between 0 for low quality to 100 for best quality.

#### Parameters

| Name | Type | Description |
| - | - | - |
| quality (optional) | integer | Encoding quality ranging from `0` to `100`. By default 75. |
| progressive (optional) | boolean | Option to encode the image in progressive Jpeg format. Disabled by default. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading gif image
$image = $manager->read('images/example.gif');

// encoding jpeg data
$encoded = $image->toJpeg(90); // Intervention\Image\EncodedImage
```

### Encoding WebP Format

> public Image::toWebp(int $quality = 75): EncodedImage

Encode the current image instance in the WebP graphic format in the given **quality** ranging between 0 for low quality to 100 for best quality.

#### Parameters

| Name | Type | Description |
| - | - | - |
| quality (optional) | integer | Encoding quality. 75 by default. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading gif image
$image = $manager->read('images/example.gif');

// encoding jpeg data
$encoded = $image->toWebp(60); // Intervention\Image\EncodedImage
```

### Encoding PNG Format

> public Image::toPng(bool $interlaced = false, bool $indexed = false): EncodedImage

This method encodes the current image instance in PNG format. Further details
of the format can be defined via the parameters. It is possible to set the
encoding method for the PNG image to `interlaced`, which means the image can be
progressively rendered; non-interlaced sequential saving is used here by
default.

The second option `indexed` determines whether the image is saved with an
indexed (limited) color palette. With this option, the colors are automatically
reduced, which results in smaller file sizes, but can also lead to a loss of
quality in the coloring. By default, the encoder always outputs truecolor
format.

**Please note that the GD driver for PNG output with indexed color palette only
supports binary transparency.** This means that colors can either be completely
transparent or completely opaque. Semi-transparency is not possible with GD.

| Name | Type | Description |
| - | - | - |
| interlaced (optional) | bool | Option to encode the image interlaced. Disabled by default. |
| indexed (optional) | bool | Option for encoding PNG format with an indexed color palette. True color (non-indexed) by default. |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading jpg image
$image = $manager->read('images/example.jpg');

// encoding as truecolor png image
$encoded = $image->toPng(); // Intervention\Image\EncodedImage

// encoding png format with and indexed color palette
$encoded = $image->toPng(indexed: true); // Intervention\Image\EncodedImage
```

### Encoding GIF Format

> public Image::toGif(bool $interlaced = false): EncodedImage

Encode the current image instance in GIF format.

**Caution: The signature has changed in version 3.1 by removing the parameter `color_limit`**

| Name | Type | Description |
| - | - | - |
| interlaced (optional) | bool | Option to encode the image interlaced. Disabled by default. |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading jpg image
$image = $manager->read('images/example.jpg');

// encoding gif data
$encoded = $image->toGif(); // Intervention\Image\EncodedImage
```

### Encoding Windows Bitmap Format

> public Image::toBitmap(): EncodedImage

Encode the current image instance in Windows Bitmap format.

**Caution: The signature has changed in version 3.1 by removing the parameter `color_limit`**

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading jpg image
$image = $manager->read('images/example.jpg');

// encoding bitmap data
$encoded = $image->toBmp(); // Intervention\Image\EncodedImage
```

### Encoding AV1 Image File Format (AVIF)

> public Image::toAvif(int $quality = 75): EncodedImage

Encode the current image instance in AVIF format in the given **quality**
ranging between 0 for low quality to 100 for best quality.

| Name | Type | Description |
| - | - | - |
| quality (optional) | integer | Encoding quality. 75 by default. |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading jpg image
$image = $manager->read('images/example.jpg');

// encode avif image 
$encoded = $image->toAvif(60); // Intervention\Image\EncodedImage
```

### Encoding TIFF Format

> public Image::toTiff(int $quality = 75): EncodedImage

Encode the current image instance in TIFF format in the given **quality**
ranging between 0 for low quality to 100 for best quality.

| Name | Type | Description |
| - | - | - |
| quality (optional) | integer | Encoding quality. 75 by default. |

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading jpg image
$image = $manager->read('images/example.jpg');

// encode tiff format
$encoded = $image->toTiff(60); // Intervention\Image\EncodedImage
```

### Encoding JPEG 2000 Format

> public Image::toJpeg2000(int $quality = 75): EncodedImage

Encode the current image instance in JPEG 2000 format in the given **quality**
ranging between 0 for low quality to 100 for best quality.

| Name | Type | Description |
| - | - | - |
| quality (optional) | integer | Encoding quality. 75 by default. |

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// reading png format
$image = $manager->read('images/example.png');

// encode jpeg 2000 format
$encoded = $image->toJpeg2000(90); // Intervention\Image\EncodedImage
```




### Encoding Heic Format

> public Image::toHeic(int $quality = 75): EncodedImage

Encode the current image instance in HEIC format in the given **quality** ranging between 0 for low quality to 100 for best quality.

| Name | Type | Description |
| - | - | - |
| quality (optional) | integer | Encoding quality. 75 by default. |

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// reading png format
$image = $manager->read('images/example.jpg');

// encode heic image
$encoded = $image->toHeic(60); // Intervention\Image\EncodedImage
```




## Handling of Encoded Image Data

The mentioned encoding methods return an `Intervention\Image\EncodedImage`
object. With this instance you can decide how to proceed with the encoded data.

### Cast Encoded Image Data to String

> public EncodedImage::__toString(): string

This method can be used to obtain the raw image data as type string. This is
particularly useful if it is to be further processed with other libraries or
transferred to remote data storage (such as S3).

#### Example

```php
use Intervention\Image\ImageManager;
use Just\An\Example\CloudStorage;

// create new manager instance with desired driver
$manager = ImageManager::imagick();

// resize gif image
$image = $manager
    ->read('images/example.gif')
    ->scale(height: 200);

// encode in jpeg format and cast result as string
$imagedata = (string) $image->toJpeg();

// save to imaginary data service
CloudStorage::put('example.jpg', $imagedata);
```



### Saving Encoded Image Data in Filesystem

> public EncodedImage::save(string $filepath, mixed ...$options): void

This method writes the object's data to the given path in the local file system. The
respective folder structure must already exist and be writable.

#### Parameters

| Name | Type | Description |
| - | - | - |
| filepath | string | Path to file in filesystem. |
| options (optional) | mixed | Option parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading gif image
$image = $manager->read('images/example.gif');

// save progressive jpeg file in low quality
$encoded = $image->toJpeg()->save('images/test.jpg', progressive: true, quality: 10);
```


### Creating Data URI scheme

> public EncodedImage::toDataUri(): string

This method takes the already encoded image data and wraps it in an base64 encoded data uri scheme. 

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading gif image
$image = $manager->read('images/example.gif');

// encoding to gif data uri
$data_uri = $image->toGif()->toDataUri();
```

### Transform Encoded Image to File Pointer

> public EncodedImage::toFilePointer()

Create a file pointer to handle the encoded image data.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading gif image
$image = $manager->read('images/example.gif');

// create file pointer
$pointer = $image->toJpeg()->toFilePointer();
```

### Retrieve Media (MIME) Type of an Encoded Image

> public EncodedImage::mediaType(): string

This method returns the media (MIME) type of the encoded image.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// reading gif image
$image = $manager->read('images/example.gif');

// "image/jpeg"
$mimetype = $image->toJpeg()->mediaType();
```









## Writing Images Directly

### Encoding & Saving Combined

> public Image::save(?string $path = null, mixed ...$options): ImageInterface

This method helps to initiate the saving process directly from the image object
without having to go via an `EncodedImage` object and encodes & writes the
image data in one call.

The resulting image format is defined by the file extension of the given path.
If no path is given the format of the originally read image will be used.
Define the image quality by using the second parameter.

The encoded image is saved at the given path in the local file system. The respective
folder structure must already exist and be writable.

In contrast to the other encoding methods, `save()` returns an `Image` object instead of an
`EncodedImage` object.

#### Parameters

| Name | Type | Description |
| - | - | - |
| path (optional) | null or string | File path from which the target format is extracted. By default the original path is used. |
| options (optional) | mixed | Option parameters depending on the output format. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading jpeg image
$image = $manager->read('images/example.jpg');

// overwrite file at "images/example.jpg" with low quality
$image->save(quality: 10);

// encode jpeg as png and save in a new file
$image->save('images/example.png');

// encode & save progressive jpeg in low quality
$image->save('images/example.jpg', quality: 10, progressive: true);
```

