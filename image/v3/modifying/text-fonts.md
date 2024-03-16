# Text + Fonts
## Writing text to an Image

[TOC]

## Writing Text

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


#### Examples

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = ImageManager::gd()->read('images/example.jpg');

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

// create test image
$image = ImageManager::imagick()->read('images/example.jpg');

// write text to image
$image->text('The quick brown fox', 120, 100, function (FontFactory $font) {
    $font->filename('./fonts/comic-sans.ttf');
    $font->size(70);
    $font->color('fff');
    $font->stroke('ff5500', 2);
    $font->align('center');
    $font->valign('middle');
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

> public FontFactory::filename(string $filename): FontFactory

Set a path to a font file in the file system for the text.

#### Parameters

| Name | Type | Description |
| - | - | - |
| filename | string | Path to a valid font file |

### Color

> public FontFactory::color(mixed $color): FontFactory

Define the text color in one of the valid [color formats](/v3/introduction/formats#color-formats).

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | mixed | Desired color of text |

### Text Stroke (Outline)

> public FontFactory::stroke(mixed $color, int $width = 1): FontFactory

Add an outline effect in the desired color to the text to be written. You can
also determine the width of the strokes for text characters.

**Please note that if the stroke function is used, for technical reasons it is
only possible to use fully opaque colors for text and strokes.**

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | mixed | Color of strokes in valid [color format(/v3/introduction/formats/#color-formats) |
| width | int | Optional width of the stroke effect in the range from `0` to `10` (default `1`) |

### Horizontal Alignment

> public FontFactory::align(string $align): FontFactory

Define the horizontal alignment of the text to be written starting from the
base point. Possible values are left, right and center. Default: `left`

#### Parameters

| Name | Type | Description |
| - | - | - |
| align | string | Horizontal text alignment |

### Vertical Alignment

> public FontFactory::valign(string $valign): FontFactory

Define the vertical alignment of the text to be written starting from the base
point. Possible values are top, bottom and middle. Default: `bottom`

#### Parameters

| Name | Type | Description |
| - | - | - |
| valign | string | Vertical text alignment |

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

