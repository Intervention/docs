# Image Output
## Encoding images in different formats

[TOC]

## Encoding Images

### Encoding JPEG Format

> public Image::toJpeg(int $quality = 75): EncodedImage

Encode the current image instance in JPEG format in the given **quality** ranging between 0 for low quality to 100 for best quality.

#### Parameters

| Name | Type | Description |
| - | - | - |
| quality (optional) | integer | Encoding quality  |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

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
| quality (optional) | integer | Encoding quality |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading gif image
$image = $manager->read('images/example.gif');

// encoding jpeg data
$encoded = $image->toWebp(60); // Intervention\Image\EncodedImage
```

### Encoding PNG Format

> public Image::toPng(int $color_limit = 0): EncodedImage

Encode the current image instance in PNG format. Optionally you can reduce the
colors in the final result to the given limit. If the limit falls below
256, the PNG is output with an indexed color palette.

| Name | Type | Description |
| - | - | - |
| color_limit (optional) | integer | Maximal number of colors in encoded image |

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading jpg image
$image = $manager->read('images/example.jpg');

// encoding png image with a maximal color count of 32
$encoded = $image->toPng(32); // Intervention\Image\EncodedImage
```

### Encoding GIF Format

> public Image::toGif(int $color_limit = 0): EncodedImage

Encode the current image instance in GIF format. Pass a color limit to reduce
the colors in the final result.

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading jpg image
$image = $manager->read('images/example.jpg');

// encoding gif data
$encoded = $image->toGif(24); // Intervention\Image\EncodedImage
```

### Encoding Windows Bitmap Format

> public Image::toBitmap(int $color_limit = 0): EncodedImage

Encode the current image instance in Windows Bitmap format. Pass a color limit
to reduce the colors in the final result.

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

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
| quality (optional) | integer | Encoding quality  |

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading jpg image
$image = $manager->read('images/example.jpg');

// encode avif image 
$encoded = $image->toAvif(60); // Intervention\Image\EncodedImage
```

## Handling of Encoded Image Data

All mentioned methods return an `Intervention\Image\EncodedImage` object. With this instance you can decide how to proceed with the encoded data.

### Saving encoded image data in filesystem

> public EncodedImage::save(string $filepath): void

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

#### Parameters

| Name | Type | Description |
| - | - | - |
| filepath | string | Path to file in filesystem |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'gd']);

// reading gif image
$image = $manager->read('images/example.gif');

// saving jpeg file
$encoded = $image->toJpeg()->save('images/test.jpg');
```


### Creating Data URI scheme

> public EncodedImage::toDataUri(): string

This method takes the already encoded image data and wraps it in an base64 encoded data uri scheme. 

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// reading gif image
$image = $manager->read('images/example.gif');

// encoding to gif data uri
$data_uri = $image->toGif()->toDataUri();
```

### Transform encoded image to file pointer

> public EncodedImage::toFilePointer()

Create a file pointer to handle the encoded image data.

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// reading gif image
$image = $manager->read('images/example.gif');

// create file pointer
$pointer = $image->toJpeg()->toFilePointer();
```

### Retrieve MIME Type of an encoded image

> public EncodedImage::mimetype(): string

This method takes the already encoded image data and wraps it in an base64 encoded data uri scheme. 

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);

// reading gif image
$image = $manager->read('images/example.gif');

// "image/jpeg"
$mimetype = $image->toJpeg()->mimetype();
```
