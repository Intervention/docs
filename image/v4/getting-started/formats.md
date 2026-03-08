---
title: "Supported Formats"
subtitle: "Image and Color Formats"
lead: "Learn about supported formats in Intervention Image, including image formats and various color specifications. Discover how to check runtime format support, create transparent images, and handle color spaces."
sort: 4
---

[TOC]

## Image Formats

The supported image formats depend on the used driver. While with Imagick and
libvips it is possible to read all formats that the library itself supports and
write the formats listed below with GD only the formats listed below are
readable and writable.

Read more about [encoding different image formats](/v4/basics/image-output) in the output section.

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
| ICO | ❌ | ✅ | ✅ |

**Please note that not all image formats are always included in the PHP image
extensions. It is therefore possible, that the GD library is installed but is
built without Jpeg support or Imagick is available without Webp support
for example.**

All image formats can be read from various sources. These are in detail:

- Path in filesystem
- Raw binary image data
- Base64 encoded image data
- Data Uri Scheme
- Stream resource
- `SplFileInfo` from which `Illuminate\Http\UploadedFile` and `Symfony\Component\HttpFoundation\File\UploadedFile` extend
- Intervention Image Instance (`Intervention\Image\Image`)
- Encoded Intervention Image (`Intervention\Image\EncodedImage`)
- Driver-specific image (instance of `GDImage` or `Imagick`)

### Check the Support for Image Formats

> public DriverInterface::supports(string|Format|FileExtension|MediaType $identifier): bool;

This method can be used during runtime to find out whether a specific format
is supported. It checks if the desired format is supported by the current driver and if the underlying extension has been built with the
necessary support, returning `true` if both conditions are met or `false` if the driver has no support.

#### Parameters

| Name | Type | Description |
| - | - | - |
| identifier | string, Format, FileExtension or MediaType | Identifier of the image format, which can be passed either as a file extension string, media type string or enum member.  |

#### Example

```php
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Format;
use Intervention\Image\MediaType;
use Intervention\Image\FileExtension;

$manager = ImageManager::usingDriver(Driver::class);

// check by file extension if driver supports jpeg format
$result = $manager->driver->supports('jpg');

// check by media type if driver supports jpeg format
$result = $manager->driver->supports('image/jpeg');

// check by enum member if driver supports jpeg format
$result = $manager->driver->supports(Format::JPEG);

// check by enum member if driver supports jpeg format
$result = $manager->driver->supports(MediaType::IMAGE_JPEG);

// check by enum member if driver supports jpeg format
$result = $manager->driver->supports(FileExtension::JPG);
```

## Color Formats

The library supports several formats to define colors for its methods.

The input values for colors may differ from the actual color space of the
image. Therefore, it is possible to draw on a CMYK image using an HSV
color specification. The colors will be automatically converted to the target color
space.

### Color Objects

Colors are defined in object form implementing `ColorInterface::class` building a
separate color class for each color space.

Each color object takes constructor parameters for the color channel values as well as an
optional alpha channel parameter, which is defined as completely opaque by default.

#### Create Colors from Channel Values

The easiest way is to use the static methods of `Intervention\Image\Color` to create colors in different color spaces.

```php
use Intervention\Image\Color;

// create different colors
$rgb = Color::rgb(255, 55, 0, .5);
$hsl = Color::hsl(340, 55, 90);
$hsv = Color::hsv(240, 35, 10);
$oklab = Color::oklab(0.7, 0.04, -0.09);
$oklab = Color::oklch(0.7, 0.1, 232);
$cmyk = Color::cmyk(100, 50, 70, 0, .75);
```

Of course you can use the object constructor to create colors as well.

```php
use Intervention\Image\Colors\Rgb\Color as RgbColor;
use Intervention\Image\Colors\Hsl\Color as HslColor;
use Intervention\Image\Colors\Hsv\Color as HsvColor;
use Intervention\Image\Colors\Oklab\Color as OklabColor;
use Intervention\Image\Colors\Oklch\Color as OklchColor;
use Intervention\Image\Colors\Cmyk\Color as CmykColor;

$rgb = new RgbColor(255, 55, 0, .5);
$hsl = new HslColor(340, 55, 90);
$hsv = new HsvColor(240, 35, 10);
$oklab = new OklabColor(0.7, 0.04, -0.09);
$oklab = new OklchColor(0.7, 0.1, 232);
$cmyk = new CmykColor(100, 50, 70, 0, .75);
```

### String Format

#### Functional String Format

Color formats in string format for example in the functional notation are also readable using `Intervention\Image\Color::parse()` as shown in the following example.

```php
use Intervention\Image\Color;

// universal parsing of color strings
$rgb = Color::parse('rgb(34, 12, 64)');
$hsl = Color::parse('hsl(30, 100%, 50%)');
$oklab = Color::parse('oklab(59.69% 0.1007 0.1191)');
$oklch = Color::parse('oklch(59.69% 0.156 49.77');
$oklch = Color::parse('oklch(59.69% 0.156 49.77 / .5');
```

#### Hexadecimal RGB Format

You can parse colors as RGB hex triplets, which are commonly used in HTML and
CSS. It's possible to use the shorthand as well as the full format with or
without an alpha channel. The leading `#` is optional.

```php
use Intervention\Image\Color;

// create color objects from hexadecimal rgb format
$rgb = Color::parse('b53717');
$rgb = Color::parse('b5371766');
$rgb = Color::parse('#ccc');
$rgb = Color::parse('#ccca');
```

#### Named CSS Colors

Intervention Image can read named colors from the [extended 140 HTML color
names](https://en.wikipedia.org/wiki/Web_colors#HTML_color_names) from the W3C
specification. You can pass the color names either as a string or enum value.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Colors\Rgb\NamedColor;

// use enum to define named color
$image = ImageManager::usingDriver(Driver::class)
    ->createImage(300, 200)
    ->fill(NamedColor::STEELBLUE);

// use string value to define named color
$image = ImageManager::usingDriver(Driver::class)
    ->createImage(300, 200)
    ->fill('steelblue');
```

#### Transparency

If it is necessary to specify transparency as a color, this can always be done with the `transparent()` method which returns the fully transparent RGB color `#ffffff00`.

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Color;

$image = ImageManager::usingDriver(Driver::class)
    ->decodePath('images/example.png')
    ->containDown(300, 200, Color::transparent());
```


## Colorspaces

The available color spaces are primarily determined by the used driver. The
Imagick driver supports both RGB and CMYK color spaces, whereas the GD
driver only supports RGB. The default color space for newly created images is
RGB.

Using the GD driver in Intervention Image to read CMYK images will
automatically convert them to the RGB color space, which may result in color
deviations.

Because the GD driver does not support CMYK, it is not recommended for use with
CMYK images.

Read how to read an modify colorspace in the section about [Meta
Information](/v4/basics/meta-information).

### Convert Colors to Other Colorspaces or Formats

Colors can always be converted to the supported color spaces. This is possible
even if the driver does not support the desired color space.

Color objects can also be converted between the following color spaces.

- `Intervention\Image\Colors\Rgb\Colorspace`
- `Intervention\Image\Colors\Cmyk\Colorspace`
- `Intervention\Image\Colors\Hsv\Colorspace`
- `Intervention\Image\Colors\Hsl\Colorspace`
- `Intervention\Image\Colors\Oklab\Colorspace`
- `Intervention\Image\Colors\Oklch\Colorspace`

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Colors\Cmyk\Colorspace as Cmyk;

// read RGB image from filesystem
$image = ImageManager::usingDriver(Driver::class)->decode('rgb_image.jpg');

// retrieve color of pixel at given position
$color = $image->colorAt(100, 100);

// convert color to cmyk format
$color = (string) $color->toColorspace(Cmyk::class); // 'cmyk(220 10 65 0)'
```
