# Meta Information
## Reading meta data from images

[TOC]

## Image Sizes

### Reading the pixel width

> public Image::width(): integer

Reading the width in pixels from an image instance.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->make('images/example.png');

// reading the image width
$width = $image->width();
```

### Reading the pixel height

> public Image::width(): integer

Reading the pixel height from an image instance.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->make('images/example.png');

// reading the image height
$height = $image->height();
```

### Reading the image size as an object

> public Image::size(): SizeInterface

Reading the image size from an instance.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager('gd');

// reading an image
$image = $manager->make('images/example.png');

// reading image size
$size = $image->size();

// read aspect ratio
$ratio = $size->getAspectRatio();
```

