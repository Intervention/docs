# Supported formats
## Readable image and color formats

[TOC]

## Image Formats

The readable image formats depend on the used driver. While with Imagick it is
possible to read all formats that the library itself supports, with GD only the
formats JPG, WebP, GIF, PNG, BMP and AVIF are readable and writable.

Both drivers of Intervention Image are able to decode & encode the following
image formats. Read more about image encoding in the [output
section](/v3/basics/image-output).

### JPEG

JPEG is still the most used image format of the internet. GD and Imagick driver
of Intervention Image support encoding & decoding.

```php
// encode and save an image instance in jpeg format
$image->toJpeg()->save('images/example.jpg');
```

### WebP

Encoding & decoding of the WebP graphic format is supported by GD and Imagick
driver.

```php
// encode and save an image instance in webp format
$image->toWebp()->save('images/example.webp');
```

### GIF

Since version 3 of Intervention Image there is full support for encoding &
decoding of (**animated**) GIF files with GD and Imagick driver.

```php
// encode and save an image instance in gif format
$image->toGif()->save('images/example.gif');
```

### PNG

Encoding & Decoding of PNG formated images is supported by all drivers.

```php
// encode and save an image instance in png format
$image->toPng()->save('images/example.png');
```

### AV1 Image File Format (AVIF)

Encoding & Decoding of AVIF formated images is supported by all drivers.

```php
// encode and save an image instance in ms windows bitmap format
$image->toAvif()->save('images/example.avif');
```

### Windows Bitmap

Encoding & Decoding of BMP formated images is supported by all drivers.

```php
// encode and save an image instance in ms windows bitmap format
$image->toBitmap()->save('images/example.bmp');
```

## Color Formats

The library supports several formats to define colors for its methods.

The input values for colors can deviate from the actual color space of the
image. It is therefore possible, to draw on an image in CMYK space with an HSV
color specification. The colors are automatically converted to the target color
space.

### Hexadecimal Format

You can pass colors as a RGB hex triplet used normally in HTML and CSS. It's
possible to use the shorthand as well as the full format with or without alpha
channel. The leading `#` is optional.

```php
// create new image with red background
$image = (new ImageManager(['driver' => 'gd']))->create(300, 200)->fill('b53717');

// create new image with half transparent red background
$image = (new ImageManager(['driver' => 'gd']))->create(300, 200)->fill('b5371766');
```
### String Format

#### RGB strings

RGB string values in functional notations are also supported. If you want to
include an alpha value use the RGBA prefix like in the following example.

```php
// create new image with half transparent background
$image = (new ImageManager(['driver' => 'gd']))->create(300, 200)->fill('rgba(15, 20, 255, .5)');

// create new image with red background
$image = (new ImageManager(['driver' => 'gd']))->create(300, 200)->fill('rgb(255, 0, 0)');
```

#### CMYK strings

CMYK string values in functional notations are also supported.

```php
// create new image with background
$image = (new ImageManager(['driver' => 'gd']))->create(300, 200)->fill('cmyk(100, 100, 55, 60)');
```

#### HSV/HSB strings

It is also possible to pass color values strings in the RGB alternative HSV/HSB.

```php
// create new image with half transparent background
$image = ImageManager::imagick()->read('example.jpg');

// draw colored pixel
$image->drawPixel(120, 200, 'hsv(230, 15, 75)');
```

### HTML Color Names

Intervention Image can read colors from the [extended 140 HTML color
names](https://en.wikipedia.org/wiki/Web_colors#HTML_color_names) from the W3C
specification.

```php
// create new image with half transparent background
$image = (new ImageManager(['driver' => 'gd']))->create(300, 200)->fill('steelblue');
```

## Colorspaces

The available colorspaces are primarily determined by the driver in use. The
Imagick driver is compatible with RGB and CMYK colorspaces, while the GD driver
only supports the RGB colorspace. The default colorspace for newly created
images is RGB.

When using the GD driver in Intervention Image to read CMYK images, they will
be automatically converted to the RGB colorspace, which can lead to color
deviations.

Because the GD Driver does not support CMYK color space by default, it is not
recommended to use it with CMYK images.

Read how to read an modify colorspace in the section about [Meta
Information](/v3/basics/meta-information).

### Converting Colors to other Colorspaces or formats

Colors can always be converted to the supported color spaces. This is also
possible if the driver does not support this color space.

Although the two drivers only support RGB and CMYK color spaces, color objects
can also be converted into the following formats.

- `Intervention\Image\Colors\Rgb\Colorspace`
- `Intervention\Image\Colors\Cmyk\Colorspace`
- `Intervention\Image\Colors\Hsv\Colorspace`

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Colors\Hsv\Colorspace as HsvColorspace;

// read RGB image from filesystem
$manager = new ImageManager(new Driver());
$image = $manager->read('example.jpg');

// retrieve color of pixel at given position
$color = $image->pickColor(100, 100);

// convert color to HSV format
$color = (string) $color->convertTo(HsvColorspace::class); // 'hsv(220, 10, 65)'
```
