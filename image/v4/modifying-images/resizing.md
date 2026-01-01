---
title: "Resize Images"
subtitle: "Change the Image Size in Different Ways"
lead: "Discover comprehensive image resizing techniques with the Intervention Image library. Learn methods for scaling, cropping, padding, and adjusting image canvas sizes, all while maintaining aspect ratios."
sort: 0
---

[TOC]

## Simple Image Resizing

<a href="/v3/playground#resize" target="playground" class="demoButton">Try it out in the live demo</a>

### Resize an Image

> public Image::resize(null|int $width = null, null|int $height = null): ImageInterface

The method `resize()` simply stretches the image to the desired size regardless of the original aspect ratio. Use
`resizeDown()` to change the size but do not exceed the original size of the
image. The method supports [named arguments](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments)
to target only one axis for the modification. 

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |

#### Example

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = ImageManager::imagick()->read('images/example.jpg');

// resize to 300 x 200 pixel
$image->resize(300, 200);

// resize only image height to 200 pixel
$image->resize(height: 200);
```

<a href="/v3/playground#resizeDown" target="playground" class="demoButton">Try it out in the live demo</a>

### Resize Without Exceeding the Original Size

> public Image::resizeDown(null|int $width = null, null|int $height = null): ImageInterface

The `resizeDown()` method does the same as `resize()`. It simply stretches the
image to the specified size, but does not exceeds the original size of the image. You can
use [named arguments](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments)
to resize just one axis for the modification. 

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |

#### Example

```php
use Intervention\Image\ImageManager;

// create new image instance (800 x 600)
$image = ImageManager::imagick()->read('images/example.jpg');

$image = $image->resizeDown(2000, 100); // 800 x 100

// resize only image width to 200 pixel and do not exceed the original width
$image->resizeDown(width: 200);
```

## Scale Images

<a href="/v3/playground#scale" target="playground" class="demoButton">Try it out in the live demo</a>

### Resize Images Proportionally

> public Image::scale(null|int $width = null, null|int $height = null): ImageInterface

Often you want to resize an image without distorting the original image
aspect ratio. For this kind of modification you can simply use the methods
`scale()` or `scaleDown()`.

Note that the resulting size may differ from the given arguments,
as the aspect ratio is preferably preserved.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

$manager = new ImageManager(new Driver());

// create new image instance with 800 x 600 (4:3)
$image = $manager->read('images/example.jpg');

// scale to fixed height
$image->scale(height: 300); // 400 x 300 (4:3)

// scale to 120 x 100 pixel
$image->scale(120, 100); // 120 x 90 (4:3)
```

<a href="/v3/playground#scaleDown" target="playground" class="demoButton">Try it out in the live demo</a>

### Scale Images but do not Exceed the Original Size

> public Image::scaleDown(null|int $width = null, null|int $height = null): ImageInterface

The method `scale()` resizes the image while maintaining the original aspect ratio. While
`scaleDown()` is similar to `scale()` the only difference is that it doesn't exceed the original size of the
image. The method support [named arguments](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments)
to target only one axis for the modification. 

Note that the size of the result may differ from the given parameter values.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |
#### Example


```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new image instance
$manager = new ImageManager(Driver::class);
$image = $manager->read('images/example.jpg'); // 800 x 600

// scale down to fixed width
$image->scaleDown(width: 200); // 200 x 150

// scale down to fixed height
$image->scaleDown(height: 300); //  400 x 300
```

## Fitted Image Resizing

<a href="/v3/playground#cover" target="playground" class="demoButton">Try it out in the live demo</a>

### Cropping & Resizing Combined

> public Image::cover(int $width, int $height, string $position = 'center'): ImageInterface

The `cover()` method is a two-step combination of cropping and resizing to
achieve a given result size. This method takes the given dimensions and scales
them to the largest possible size that matches the original size. This size is
then positioned on the original and cropped before being resized to the desired
size from the arguments.

This method requires both width and height arguments. You can optional
specify a position to determine which part of the image should remain in focus.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |
| position (optional) | string | Position |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new image instance (800 x 600)
$manager = new ImageManager(Driver::class);
$image = $manager->read('images/example.jpg');

// crop the best fitting 5:3 (600x360) ratio and resize to 600x360 pixel
$img->cover(600, 360);

// crop the best fitting 1:1 ratio (200x200) and resize to 200x200 pixel
$img->cover(200, 200);

// cover a size of 300x300 and position crop on the left
$image->cover(300, 300, 'left'); // 300 x 300 px
```

<a href="/v3/playground#coverDown" target="playground" class="demoButton">Try it out in the live demo</a>

### Fitted Resizing without Exceeding the Original Size

> public Image::coverDown(int $width, int $height, string $position = 'center'): ImageInterface

This method has the same purpose and the same signature as `cover()` but the
final pixel size will never be larger than the original image. Use this if
you want to avoid upsampling your image.

Note that the size of the result may differ from the given parameter values.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |
| position (optional) | string | Position |

#### Example

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = ImageManager::imagick()->read('images/example.jpg'); // 800 x 600

// resize down to 1200x720 (5:3)
$img->coverDown(1200, 720); // 800 x 480 (5:3)

// resize down to 900x900 (1:1)
$img->coverDown(900, 900); // 600 x 600

// resize down to 900x450 (2:1) and position left
$image->coverDown(900, 450, 'left'); // 800 x 400 px
```

## Padded Image Resizing

<a href="/v3/playground#pad" target="playground" class="demoButton">Try it out in the live demo</a>

### Resizing & Padding Combined

> public Image::pad(int $width, int $height, $background = 'ffffff', string $position = 'center'): ImageInterface

Padded resizing means that the original image is scaled to fit the
defined target size without changing the aspect ratio. The original image is not
scaled up but only down.
     
Compared to the `cover()` method, this method does not create cropped areas, but
possibly new empty areas on the sides of the resulting image. These will be filled
with the given background color.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Image width. |
| height | integer | Image width. |
| background (optional) | mixed | Background color for the new areas of the image. |
| position (optional) | string | Position where the original image is placed. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new image instance
$manager = ImageManager::withDriver(new Driver());
$image = $manager->read('images/example.jpg');

// resize padded to 300 x 200
$image->pad(300, 200, 'ccc');

// resize padded with positioning
$image->pad(500, 500, position: 'top-left');
```

<a href="/v3/playground#contain" target="playground" class="demoButton">Try it out in the live demo</a>

### Padded Resizing with Upscaling

> public Image::contain(int $width, int $height, $background = 'ffffff', string $position = 'center'): ImageInterface

 This method does the same as `pad()`, but also scales up the original image if
 the target size exceeds the original size.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Image width. |
| height | integer | Image width. |
| background (optional) | mixed | Background color for the new areas of the image. |
| position (optional) | string | Position where the original image is placed. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new image instance (800 x 600)
$image = ImageManager::withDriver(Driver::class)->read('images/example.jpg');

// resize padded without upsizing
$image->contain(900, 600);

// padded resizing with grey background color
$image->contain(500, 500, 'efefef');
```


## Crop Image

<a href="/v3/playground#crop" target="playground" class="demoButton">Try it out in the live demo</a>

### Cut Out a Rectangular Part

> public Image::crop(int $width, int $height, int $offset_x = 0, int $offset_y = 0, mixed $background = 'ffffff', string $position = 'top-left'): ImageInterface

Crops a rectangular area of the current image with a given width and
height at a given position. Pass optional x, y offset coordinates to
move the crop by the specified number of pixels.

You may also specify a background color. This color is used to fill any new
areas that may be created, for example if the cropped area is larger than the
original image format.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Width of the rectangular cutout |
| height | integer | Height of the rectangular cutout |
| offset_x (optional) | int | Amount of pixels the cutout will be moved on the x-axis |
| offset_y (optional) | int | Amount of pixels the cutout will be moved on the y-axis |
| background (optional) | mixed | Color to fill any newly created areas |
| position (optional) | string | Position at which the cutout will be aligned |

**Caution: The signature has changed in version 3.3 by the additional parameter `background`**

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new image instance
$manager = new ImageManager(new Driver())
$image = $manager->read('images/example.jpg');

// cut out a 200 x 150 pixel cutout at position 45,90
$image->crop(200, 150, 45, 90);

// crop a 40 x 40 pixel cutout from the bottom-right and move it 30 pixel down
$image->crop(200, 150, 0 , 30, position: 'bottom-right');
```

## Resize Image Canvas

<a href="/v3/playground#resizeCanvas" target="playground" class="demoButton">Try it out in the live demo</a>

### Resize Image Boundaries without Resampling the Original Image

> public Image::resizeCanvas(null|int $width = null, null|int $height = null, mixed $background = 'ffffff', string $position = 'center'): ImageInterface

This function changes the size of the image borders without recalculating the
actual image. If the specified sizes are larger than the original, the image
area is added in the specified color. If the specified sizes are smaller, the
original image area is cropped. The specified position is taken into account and
determines where the original image is fixed.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | null or integer | Width of the new image area |
| height | null or integer | Height of the new image area |
| background (optional) | mixed | Background color for the new areas of the image |
| position (optional) | string | Position where the original image will be fixed |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new image instance
$manager = new ImageManager(new Driver())
$image = $manager->read('images/example.jpg');

// resize image area to 800 x 600 and fill new area with yellow
$image->resizeCanvas(800, 600, 'ff0');
```

<a href="/v3/playground#resizeCanvasRelative" target="playground" class="demoButton">Try it out in the live demo</a>

### Resize Image Boundaries Relative to the Original

> public Image::resizeCanvasRelative(null|int $width = null, null|int $height = null, mixed $background = 'ffffff', string $position = 'center'): ImageInterface

This function behaves in the same way as `resizeCanvas()`, but here you specify
relative values which are either added (positive) or subtracted (negative) from the original size.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | null or integer | Amount which will be added or subtracted to the original width |
| height | null or integer | Amount which will be added or subtracted to the original height |
| background (optional) | mixed | Background color for the new areas of the image |
| position (optional) | string | Position where the original image will be fixed |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new image instance
$manager = new ImageManager(new Driver())
$image = $manager->read('images/example.jpg');

// add 50 pixels in green at each side of the image
$image->resizeCanvas(50, 50, 'green');

// add 20 red pixels to the height at the bottom of the image
$image->resizeCanvas(height: 20, background: 'ff0000', position: 'bottom');
```



## Trim Image
### Remove Border Areas in Similar Color

> public Image::trim(int $tolerance = 0): ImageInterface

Removes border areas of the image on all sides that have a similar color. The
color similarity can be varied using the optional `tolerance` parameter.

This means that with a tolerance value of `0`, only color areas with exactly
the same value will be removed. The higher the tolerance, the more similar
color areas are included. Usually values up to `20` make sense.

**Note that the results can vary greatly depending on the driver and the
image you are processing.**

#### Parameters

| Name | Type | Description |
| - | - | - |
| tolerance | integer | Tolerance value that determines how similar in color a border area may be in order to be removed. |

#### Example

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = ImageManager::gd()->read('images/example.jpg');

// trim with a tolerance of 5
$image->trim(5);
```
