---
title: "Text & Fonts"
subtitle: "Write Text on an Image"
lead: "Learn how to add text and fonts on images with PHP and Intervention Image. Discover methods for setting font size, font color, alignment, rotation, line height, and text wrapping."
sort: 3
---

[TOC]

## Write Text

> public Image::text(string $text, int $x, int $y, callable|FontInterface $font): ImageInterface

Write a **text** string at the basepoint position of **x, y** to the current
image. You can define more details like font-size, font-file and alignment via
a callback as the fourth parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| text | string | The text that will be written to the image. |
| x | integer | Coordinate on x-axis defining the base point of the first character. |
| y | integer | Coordinate on y-axis defining the base point of the first character. |
| font | callable or FontInterface | Callback function to configure the font appearance or `Typography\Font` instance. |


#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new image instance
$image = ImageManager::usingDriver(Driver::class)->decode('images/example.jpg');

// write text at a certain position
$image->text('The quick brown fox', 120, 100);

```
## Text & Font Settings

To define the overall appearance of the text and set more details you can pass
a callback as an optional parameter. The callback places the calls on the
FontInterface and listens for following methods.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Typography\FontFactory;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Alignment;

// create test image
$image = ImageManager::usingDriver(Driver::class)->decode('images/example.jpg');

// write text to image
$image->text('The quick brown fox', 120, 100, function (FontFactory $font) {
    $font->filepath('./fonts/comic-sans.ttf');
    $font->size(70);
    $font->color('fff');
    $font->stroke('ff5500', 2);
    $font->align(Alignment::CENTER, Alignment::TOP);
    $font->lineHeight(1.6);
    $font->angle(10);
    $font->wrap(250);
});
```

### Font Size

> public FontFactory::size(float $size): FontFactory

Define a font size. By default, a value of `12` will be applied.

#### Parameters

| Name | Type | Description |
| - | - | - |
| size | float | Font size to be applied |

### Font File

> public FontFactory::filepath(string $path): FontFactory

Set a path to a font file in the file system for the text.

#### Parameters

| Name | Type | Description |
| - | - | - |
| path | string | Path to a valid font file |

### Color

> public FontFactory::color(string|ColorInterface $color): FontFactory

Define the text color in one of the valid [color formats](/v4/getting-started/formats#color-formats).

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | string or ColorInterface | Desired color of text |

### Text Stroke (Outline)

> public FontFactory::stroke(string|ColorInterface $color, int $width = 1): FontFactory

Add an outline effect in the desired color to the text to be written. You can
also determine the width of the strokes for text characters.

**Please note that if the stroke function is used, for technical reasons it is
only possible to use fully opaque colors for text and strokes.**

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | string or ColorInterface | Color of strokes in valid [color format](/v4/getting-started/formats/#color-formats) |
| width | int | Optional width of the stroke effect in the range from `0` to `10` (default `1`) |

### Horizontal Alignment

> public FontFactory::align(null|string|Alignment $horizontal = null, null|string|Alignment $vertical = null): FontFactory

Define the horizontal and vertical alignment of the text starting from the
base point. By default the text is alignment left horizontally and at the bottom vertically.

#### Parameters

| Name | Type | Description |
| - | - | - |
| horizontal | null, string or Alignment | Horizontal text alignment |
| vertical | null, string or Alignment | Vertical text alignment |

### Rotation

> public FontFactory::angle(float $angle): FontFactory

Rotate the text block clockwise with a desired angle.

#### Parameters

| Name | Type | Description |
| - | - | - |
| angle | float | Rotation angle |

### Line Height

> public FontFactory::lineHeight(float $height): FontFactory

Define the line height of the text block. Applies only to multi-line text.
Default value is `1.25`.

#### Parameters

| Name | Type | Description |
| - | - | - |
| height | float | Line height for multi-line text block |

### Text Wrapping

> public FontFactory::wrap(int $width): FontFactory

Specifies the maximum width of the text in pixels. The text to be rendered is
parsed using the specified font options, and each line is automatically wrapped
to the maximum width. Hyphenation is not performed.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | int | Maximum width of the text block |
