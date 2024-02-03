# Text + Fonts
## Writing text to an image

[TOC]

## Writing text

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
## Text & font settings

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
    $font->color('#b01735');
    $font->size(70);
    $font->align('center');
    $font->valign('middle');
    $font->lineHeight(1.6);
    $font->angle(10);
    $font->wrap(250);
});
```

### Font size

> public FontInterface::size(float $size): FontInterface

Define a font size. By default, a value of `12` will be applied.

#### Parameters

| Name | Type | Description |
| - | - | - |
| size | float | Font size to be applied |

### Font file

> public FontInterface::filename(string $filename): FontInterface

Set a path to a font file in the file system for the text.

#### Parameters

| Name | Type | Description |
| - | - | - |
| filename | string | Path to a valid font file |

### Color

> public FontInterface::color(mixed $color): FontInterface

Define the text color in one of the valid [color formats](/v3/introduction/formats#color-formats).

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | mixed | Desired color of text |

### Horizontal alignment

> public FontInterface::align(string $align): FontInterface

Define the horizontal alignment of the text to be written starting from the
base point. Possible values are left, right and center. Default: `left`

#### Parameters

| Name | Type | Description |
| - | - | - |
| align | string | Horizontal text alignment |

### Vertical alignment

> public FontInterface::valign(string $valign): FontInterface

Define the vertical alignment of the text to be written starting from the base
point. Possible values are top, bottom and middle. Default: `bottom`

#### Parameters

| Name | Type | Description |
| - | - | - |
| valign | string | Vertical text alignment |

### Rotation

> public FontInterface::angle(float $angle): FontInterface

Rotate the text block clockwise with a desired angle.

#### Parameters

| Name | Type | Description |
| - | - | - |
| angle | float | Rotation angle |

### Line height

> public FontInterface::lineHeight(float $height): FontInterface

Define the line height of the text block. Applies only to multi-line text.
Default value is `1.25`.

#### Parameters

| Name | Type | Description |
| - | - | - |
| height | float | Line height for multi-line text block |

### Text wrapping

> public FontInterface::wrap(int $width): FontInterface

Specifies the maximum width of the text in pixels. The text to be rendered is
parsed using the specified font options, and each line is automatically wrapped
to the maximum width. Hyphenation is not performed.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | int | Maximum width of the text block |

