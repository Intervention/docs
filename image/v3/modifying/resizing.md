# Resize Images
## Change the Image Size in Different Ways
Discover comprehensive image resizing techniques with the Intervention Image library. Learn methods for scaling, cropping, padding, and adjusting image canvas sizes, all while maintaining aspect ratios.

[TOC]

## Simple Image Resizing

### Resizing the Image

> public Image::resize(?int $width, ?int $height): ImageInterface

The method `resize()` simply stretches the image to the desired size. Use
`resizeDown()` to change the size but do not exceed the original size of the
image. The method support [named arguments](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments)
to target just one axis for the modification. 

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |


#### Examples

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = ImageManager::imagick()->read('images/example.jpg');

// resize to 300 x 200 pixel
$image->resize(300, 200);

// resize only image height to 200 pixel
$image->resize(height: 200);
```


### Resizing Without Exceeding the Original Size

> public Image::resizeDown(?int $width, ?int $height): ImageInterface

The method `resize()` simply stretches the image to the desired size. Use
`resizeDown()` to change the size but do not exceed the original size of the
image. The method support [named arguments](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments)
to target just one axis for the modification. 


#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |


#### Examples

```php
use Intervention\Image\ImageManager;

// create new image instance (800 x 600)
$image = ImageManager::imagick()->read('images/example.jpg');

$image = $image->resizeDown(2000, 100); // 800 x 100

// resize only image width to 200 pixel and do not exceed the origial width
$image->resizeDown(width: 200);
```

## Scaling Images

### Resizing Images Proportionally

> public Image::scale(?int $width, ?int $height): ImageInterface

Often you want to resize an image but do not want to distort the original image
aspect ratio. For this kind of modification you can simply use the methods
`scale()` or `scaleDown()`.

Keep in mind that the resulting size may differ from the given arguments,
because the aspect ratio will be maintained preferably.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |


#### Examples

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

### Scaling Images but do not Exceed the Original Size

> public Image::scaleDown(?int $width, ?int $height): ImageInterface

The method `scale()` resizes the image and maintains the aspect ratio. While
`scaleDown()` is similar to `scale()` the only difference is it doesn't exceed the original size of the
image. The method support [named arguments](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments)
to target just one axis for the modification. 

Please note that the size of the result may differ from the given parameter values.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |


#### Examples

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

### Cropping & Resizing Combined

> public Image::cover(int $width, int $height, string $position = 'center'): ImageInterface

The `cover()` method is a two step combination of trimming excess pixels and
resizing to achieve a certain result size. This method takes the given
dimensions and scales it to the largest possible size matching the original
size. Then this size is positioned on the original and cut out before being
resized to the desired size from the arguments.

For this method both width and height arguments are required. You can optional
set a position to determine which part of the image should remain in focus.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |
| position (optional) | string | Position |


#### Examples

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

### Fitted Resizing without Exceeding the Original Size

> public Image::coverDown(int $width, int $height, string $position = 'center'): ImageInterface

This method has the same purpose and the same signature as `cover()` but the
end result pixel size will never be larger than the original image. Use this if
you want to prevent up-sampling your image.

Please note that the size of the result may differ from the given parameter values.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |
| position (optional) | string | Position |

#### Examples

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

### Resizing & Padding Combined

> public Image::pad(int $width, int $height, $background = 'ffffff', string $position = 'center'): ImageInterface

Padded resizing means that the original image is scaled until it fits the
defined target size with unchanged aspect ratio. The original image is not
scaled up but only down.
     
Compared to the `cover()` method, this method does not create cropped areas, but
possibly new empty areas on the sides of the result image. These are filled
with the specified background color.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Image width. |
| height | integer | Image width. |
| background (optional) | mixed | Background color for the new areas of the image. |
| position (optional) | string | Position where the original image is placed. |


#### Examples

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

### Padded Resizing with Upscaling

> public Image::contain(int $width, int $height, $background = 'ffffff', string $position = 'center'): ImageInterface

 This method does the same as `pad()`, but the original image is also scaled
 up if the target size exceeds the original size.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Image width. |
| height | integer | Image width. |
| background (optional) | mixed | Background color for the new areas of the image. |
| position (optional) | string | Position where the original image is placed. |


#### Examples

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
### Cut Out a Rectangular Part

> public Image::crop(int $width, int $height, int $offset_x = 0, int $offset_y = 0, mixed $background = 'ffffff', string $position = 'top-left'): ImageInterface

Cuts a rectangular portion of the current image with a given width and
height at a specified position. Pass optional x, y offset coordinates to
move the crop by the specified number of pixels.

You can also specify a background color. This color is used to fill any new
areas that may be created, e.g. if the cropped area is larger than the original
image format.


#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Width of the rectangular cutout |
| height | integer | Height of the rectangular cutout |
| offset_x (optional) | int | Amount of pixels the cutout will be moved on the x-axis |
| offset_y (optional) | int | Amount of pixels the cutout will be moved on the y-axis |
| background (optional) | mixed | Color to fill any newly created areas |
| position (optional) | string | Position at which the cutout will be aligned |

**Caution: The signature has changed in version 3.3 by adding the parameter `background`**

#### Examples

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
### Resize Image Boundaries without Resampling the Original Image

> public Image::resizeCanvas(?int $width, ?int $height, mixed $background = 'ffffff', string $position = 'center'): ImageInterface

This function changes the size of the image borders without recalculating the
actual image. If the specified sizes are larger than the original, the image
area is added in the specified color. If the specified sizes are smaller, the
original image area is cropped. The given position is taken into account and
determines where the original image is fixed.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | null or integer | Width of the new image area |
| height | null or integer | Height of the new image area |
| background (optional) | mixed | Background color for the new areas of the image |
| position (optional) | string | Position where the original image will be fixed |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new image instance
$manager = new ImageManager(new Driver())
$image = $manager->read('images/example.jpg');

// resize image area to 800 x 600 and fill new area with yellow
$image->resizeCanvas(800, 600, 'ff0');
```

### Resize Image Boundaries Relative to the Original

> public Image::resizeCanvasRelative(?int $width, ?int $height, mixed $background = 'ffffff', string $position = 'center'): ImageInterface

This function behaves in the same way as `resizeCanvas()`, but here relative values are
specified which are either added or subtracted from the original size.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | null or integer | Amount which will be added or subtracted to the original width |
| height | null or integer | Amount which will be added or subtracted to the original height |
| background (optional) | mixed | Background color for the new areas of the image |
| position (optional) | string | Position where the original image will be fixed |

#### Examples

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

Remove border areas of the image on all sides that have a similar color. The
similarity of the color can be varied using the optional `tolerance` parameter.

This means that with a tolerance value of `0`, only color areas that have exactly
the same value are removed. As the tolerance increases, similar color areas are also
included and cut off. Usually values up to `20` make sense.

**Please note that the results can vary greatly depending on the driver and the
image you are processing.**

#### Parameters

| Name | Type | Description |
| - | - | - |
| tolerance | integer | Tolerance value that determines how similar in color a border area may be in order to be removed. |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = ImageManager::gd()->read('images/example.jpg');

// trim with a tolerance of 5
$image->trim(5);
```

