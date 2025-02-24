# Insert Images
## Place Images onto other Images
Learn how to insert images onto other images using the Intervention Image library. Position images, adjust offsets, and control opacity for custom overlays or watermarks.

[TOC]

## Insert Images

> public Image::place(mixed $element, string $position = 'top-left', int $offset_x = 0, int $offset_y = 0, int $opacity = 100): ImageInterface

Places an image at the specified position. The image to be inserted can be
specified from any of the [supported image sources](/v3/basics/instantiation#reading-image-sources). 
Optionally, you can pass coordinates for an offset to move the image relative to the specified
position. It is also possible to control the opacity of the "watermark" with
the `opacity` parameter.

The possible `position` values are:

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
| opacity | int | Control over the opacity of the placed image ranging from 0 (fully transparent) to 100 (opaque) |

#### Example

```php
use Intervention\Image\ImageManager;

// create an test image from a file
$manager = ImageManager::gd();
$image = $manager->read('test.png');

// paste another image
$img->place('images/foo.png');

// create a new resized watermark instance and insert at bottom-right 
// corner with 10px offset and an opacity of 25%
$img->place(
    'images/watermark.png',
    'bottom-right', 
    10, 
    10,
    25
);
```
