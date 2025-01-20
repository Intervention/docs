# Supported Formats
## Image and Color Formats
Learn about supported formats in Intervention Image, including image formats and various color specifications. Discover how to check runtime format support, create transparent images, and handle color spaces.

[TOC]

## Image Formats

The supported image formats depend on the used driver. While with Imagick and
libvips it is possible to read all formats that the library itself supports and
write the formats listed below with GD only the formats listed below are
readable and writable.

Read more about [encoding different image formats](/v3/basics/image-output) in the output section.

| Format | GD | Imagick | libvips |
| - | - | - | - |
| JPEG | ✅ | ✅ | ✅ |
| GIF | ✅ | ✅ | ✅ |
| Animated GIF | ✅ | ✅ | ✅ |
| PNG | ✅ | ✅ | ✅ |
| AVIF | ✅ | ✅ | ✅ |
| Bitmap | ✅ | ✅ | ✅ |
| WebP | ✅ | ✅ | ✅ |
| Animated WebP | ❌ | ✅ | ✅ |
| TIFF | ❌ | ✅ | ✅ |
| JPEG 2000 | ❌ | ✅ | ✅ |
| HEIC | ❌ | ✅ | ✅ |

**Please note that not all image formats are always included in the PHP image
extensions. It is therefore possible, that the GD library is installed but is
built without Jpeg support or Imagick is available without Webp support
for example.**

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
use Intervention\Image\Drivers\Imagick\Driver as ImagickDriver
use Intervention\Image\Format;
use Intervention\Image\MediaType;
use Intervention\Image\FileExtension;

$manager = ImageManager::withDriver(ImagickDriver::class);

// check by file extension if driver supports jpeg format
$result = $manager->driver()->supports('jpg');

// check by media type if driver supports jpeg format
$result = $manager->driver()->supports('image/jpeg');

// check by enum member if driver supports jpeg format
$result = $manager->driver()->supports(Format::JPEG);

// check by enum member if driver supports jpeg format
$result = $manager->driver()->supports(MediaType::IMAGE_JPEG);

// check by enum member if driver supports jpeg format
$result = $manager->driver()->supports(FileExtension::JPG);
```

## Color Formats

The library supports several formats to define colors for its methods.

The input values for colors may differ from the actual color space of the
image. Therefore, it is possible to draw on an image in CMYK space with an HSV
color specification. The colors are automatically converted to the target color
space.

### String Format

#### Hexadecimal String Format

You can pass colors as RGB hex triplets, which are commonly used in HTML and
CSS. It's possible to use the shorthand as well as the full format with or
without alpha channel. The leading `#` is optional.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new image with red background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('b53717');

// create new image with half transparent red background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('b5371766');
```

#### RGB String Format

RGB string values in functional notations are also supported. If you want to
include an alpha value use the RGBA prefix like in the following example.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new image with half transparent background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('rgba(15, 20, 255, .5)');

// create new image with red background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('rgb(255, 0, 0)');
```

#### CMYK String Format

CMYK string values in functional notations are also supported.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new image with background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('cmyk(100, 100, 55, 60)');
```

#### HSV/HSB String Format

It is also possible to pass color values strings in the RGB alternative HSV/HSB.

```php
use Intervention\Image\ImageManager;

// create new image with half transparent background
$image = ImageManager::imagick()->read('example.jpg');

// draw colored pixel
$image->drawPixel(120, 200, 'hsv(230, 15, 75)');
```

#### HSL String Format

It is also possible to pass color values strings in the HSL color format.

```php
use Intervention\Image\ImageManager;

// create new image with half transparent background
$image = ImageManager::imagick()->read('example.jpg');

// fill image with color
$image->fill(120, 200, 'hsl(100, 15, 10)');
```

#### HTML Color Names

Intervention Image can read colors from the [extended 140 HTML color
names](https://en.wikipedia.org/wiki/Web_colors#HTML_color_names) from the W3C
specification.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new image with half transparent background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill('steelblue');
```

#### Transparency

If it is necessary to specify transparency as a color, this can always be done
with the keyword `transparent`.

```php
use Intervention\Image\ImageManager;

$manager = ImageManager::gd();
$image = $manager->read('images/example.png');
$image->pad(300, 200, 'transparent');
```

### Color Objects

Colors can also be defined in object form. There is currently a separate color
class for each color space.

#### RGB Color Object

The RGB color object uses three parameters for the basic channels as well as an
optional alpha channel parameter, which is defined as completely opaque by
default.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Colors\Rgb\Color;

// create new image with half transparent background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill(new Color(45, 0, 10, .5));

// create new image with red background
$image = (new ImageManager(Driver::class))->create(300, 200)->fill(new Color(255, 0, 0));
```

#### CMYK Color Object

The CMYK color object is constructed using four parameters that correspond to
the four channels of the color space.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Colors\Cmyk\Color;

// create new image with half transparent background
$image = ImageManager::imagick()->create(300, 200)->fill(new Color(100, 100, 55, 60));
```

#### HSV/HSB Color Object

The HSV/HSB color object constructor takes three parameter for Hue, Saturation and Value/Brightness.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Colors\Hsv\Color;

// create new image with half transparent background
$image = ImageManager::imagick()->create(300, 200)->fill(new Color(230, 15, 75));
```

#### HSL Color Object

The HSL color object constructor takes three parameter for Hue, Saturation and Luminance.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Colors\Hsl\Color;

// create new image with half transparent background
$image = ImageManager::imagick()->create(300, 200)->fill(new Color(230, 15, 75));
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
- `Intervention\Image\Colors\Hsl\Colorspace`

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
