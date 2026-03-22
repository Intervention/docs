---
title: "Insert Images"
subtitle: "Inserting images onto other images"
lead: "Learn how to insert images onto other images using the Intervention Image library. Position images, adjust offsets, and control transparency for custom overlays or watermarks."
sort: 1
---

[TOC]

## Insert Images

> public Image::insert(mixed $image, int $x = 0, int $y = 0, string|Alignment $alignment = Alignment::TOP_LEFT, float $transparency = 1): ImageInterface

Inserts a new image on top of the current image. The image to be inserted can be specified
from any of the [supported image sources](/v4/basics/instantiation#supported-image-sources). Optionally you can
pass coordinates for an offset to move the image relative to the specified
alignment position. It is also possible to control the opacity of the insertion using the `transparency` parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| image | mixed | Source of the image to be inserted |
| x | int | Optional relative offset of the new image on x-axis |
| y | int | Optional relative offset of the new image on y-axis |
| alignment | string or `Alignment` | Alignment position of the image to be inserted |
| transparency | float | Control over the transparency of the inserted image ranging from 0 (fully transparent) to 1 (opaque) |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Alignment;

// create an test image from a file
$manager = ImageManager::usingDriver(Driver::class);
$image = $manager->decode('test.png');

// insert another image
$image->insert('images/foo.png');

// create a new resized watermark
$watermark = $manager
    ->decode('watermark.png')
    ->scale(width: 120);

// insert at bottom-right corner with 10px offset and an opacity of 25%
$image->insert(
    $watermark,
    10, 
    10,
    Alignment::BOTTOM_RIGHT, 
    .25
);
```
