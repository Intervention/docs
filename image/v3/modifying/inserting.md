# Inserting Images
## Insert images into other images

[TOC]

## Inserting Images

> public Image::place($element, string $position = 'top-left', int $offset_x = 0, int $offset_y = 0): ImageInterface

Inserts the image passed via `element` into the current image instance. The
passed element can be one of the supported image sources. The image will be
inserted at the specified position and will be shifted relative to the position
using the optional offset values.

The possible position values are:

- `top-left` (default)
- `top`
- `top-right`
- `left`
- `center`
- `right`
- `bottom-left`
- `bottom`
- `bottom-right`

#### Parameters

| Name | Type | Description |
| - | - | - |
| element | mixed | Source of the image to be placed |
| position | string | Position of the image to be placed |
| offset_x | int | Optional relative offset of the new image on x-axis |
| offset_y | int | Optional relative offset of the new image on y-axis |

#### Example

```php
// create an test image from a file
$manager = new ImageManager(['driver' => 'imagick']);
$image = $manager->read('test.png');

// paste another image
$img->place('images/foo.png');

// create a new Image instance and insert at bottom-right corner with 10px offset
$watermark = Image::make('images/watermark.png');
$img->place($watermark, 'bottom-right', 10, 10);
```
