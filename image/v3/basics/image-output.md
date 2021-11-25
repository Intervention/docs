# Image Output
## Encoding images in different formats

[TOC]

## Encoding Images

### Encoding JPEG Format

> public Image::toJpeg(int $quality = 75): EncodedImage

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

#### Parameters

| Name | Type | Description |
| - | - | - |
| quality (optional) | integer | Encoding quality  |

#### Example

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading gif image
$image = $manager->make('images/example.gif');

// encoding jpeg data
$encoded = $image->toJpeg(90); // Intervention\Image\EncodedImage
```


### Encoding PNG Format

> public Image::toPng(): EncodedImage

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

### Encoding GIF Format

> public Image::toGif(): EncodedImage

Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

#### Parameters

| Name | Type | Description |
| - | - | - |
| quality (optional) | integer | Encoding quality  |


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
$manager = new ImageManager('gd');

// reading gif image
$image = $manager->make('images/example.gif');

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
$manager = new ImageManager('imagick');

// reading gif image
$image = $manager->make('images/example.gif');

// encoding to gif data uri
$data_uri = $image->toGif()->toDataUri();
```
