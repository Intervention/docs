# Supported Formats
## Readable Image and Color Formats

[TOC]

## Image Formats

The readable image formats depend on the used driver. While with Imagick it is
possible to read all formats that the library itself supports, with GD only
some formats are readable and writable.

| Format | GD | Imagick |
| - | - | - |
| JPEG | ✅ | ✅ |
| GIF | ✅ | ✅ |
| Animated GIF | ✅ | ✅ |
| PNG | ✅ | ✅ |
| AVIF | ✅ | ✅ |
| Bitmap | ✅ | ✅ |
| WebP | ✅ | ✅ |
| Animated WebP | ❌ | ✅ |
| TIFF | ❌ | ✅ |
| JPEG 2000 | ❌ | ✅ |
| HEIC | ❌ | ✅ |

**Please note that not all image formats are always included in the PHP image
extensions. It is therefore possible, that the GD library is installed but is
built without Jpeg support or Imagick is available without Webp support
for example.**

Read more about [encoding different image formats](/v3/basics/image-output) in the output section.

### Check the Support for Image Formats

> public DriverInterface::supports(string|Format|FileExtension|MediaType $identifier): bool

This method can be used to find out during runtime whether a specific format
is supported. It checks whether the desired format is supported by the
respective driver and whether the underlying extension was built with the
corresponding support and returns `true` if both conditions apply.

#### Parameters

| Name | Type | Description |
| - | - | - |
| identifier | string, Format, FileExtension or MediaType | Identifier of the image format, which can be passed either as a file extension string, media type string or enum member.  |


#### Examples

```php
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Format;
use Intervention\Image\MediaType;
use Intervention\Image\FileExtension;

// create new driver object
$driver = new Driver();

// check if jpeg format is supported by file extension
$result = $driver->supports('jpg');

// check if gif format is supported by media type
$result = $driver->supports('image/gif');

// check if png format is supported by enum member
$result = $driver->supports(Format::PNG);

// check if avif format is supported by enum member
$result = $driver->supports(MediaType::IMAGE_AVIF);

// check if tiff format is supported by enum member
$result = $driver->supports(FileExtension::TIFF);
```

## Color Formats

The library supports several formats to define colors for its methods.

The input values for colors may differ from the actual color space of the
image. Therefore, it is possible to draw on an image in CMYK space with an HSV
color specification. The colors are automatically converted to the target color
space.

### Hexadecimal Format

You can pass colors as RGB hex triplets, which are commonly used in HTML and
CSS. It's possible to use the shorthand as well as the full format with or
without alpha channel. The leading `#` is optional.

```php
use Intervention\Image\Drivers\Imagick\Driver;

// create new image with red background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('b53717');

// create new image with half transparent red background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('b5371766');
```

### RGB String Format

RGB string values in functional notations are also supported. If you want to
include an alpha value use the RGBA prefix like in the following example.

```php
use Intervention\Image\Drivers\Gd\Driver;

// create new image with half transparent background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('rgba(15, 20, 255, .5)');

// create new image with red background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('rgb(255, 0, 0)');
```

### CMYK String Format

CMYK string values in functional notations are also supported.

```php
use Intervention\Image\Drivers\Imagick\Driver;

// create new image with background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('cmyk(100, 100, 55, 60)');
```

### HSV/HSB String Format

It is also possible to pass color values strings in the RGB alternative HSV/HSB.

```php
// create new image with half transparent background
$image = ImageManager::imagick()->read('example.jpg');

// draw colored pixel
$image->drawPixel(120, 200, 'hsv(230, 15, 75)');
```

## HTML Color Names

Intervention Image can read colors from the [extended 140 HTML color
names](https://en.wikipedia.org/wiki/Web_colors#HTML_color_names) from the W3C
specification.

```php
use Intervention\Image\Drivers\Gd\Driver;

// create new image with half transparent background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('steelblue');
```

### Transparency

If it is necessary to specify transparency as a color, this can always be done
with the keyword `transparent`.

```php
$manager = ImageManager::gd();
$image = $manager->read('images/example.png');
$image->pad(300, 200, 'transparent');
```

## Colorspaces

The available color spaces are primarily determined by the driver used. The
Imagick driver is compatible with RGB and CMYK color spaces, while the GD
driver only supports RGB. The default color space for newly created images is
RGB.

When using the GD driver in Intervention Image to read CMYK images, they will
be automatically converted to the RGB color space, which may result in color
deviations.

Since the GD driver does not support the CMYK color space by default, it is not
recommended to use it with CMYK images.

Read how to read an modify colorspace in the section about [Meta
Information](/v3/basics/meta-information).

### Converting Colors to Other Colorspaces or Formats

Colors can always be converted to the supported color spaces. This is possible
even if the driver does not support that color space.

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
