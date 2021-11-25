# Resizing Images
## Setting new image sizes

[TOC]

## Simple Image Resizing

### Resizing the image

> public Image::resize(?int $width, ?int $height): ImageInterface

The method `resize()` simply stretches the image to the desired size. Use `resizeDown()` to change the size but do not exceed the original size of the image. The method support [named arguments](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments) to target just one axis for the modification. 


#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |


#### Examples

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = (new ImageManager('gd'))->make('images/example.jpg');

// resize to 300 x 200 pixel
$image->resize(300, 200);

// resize only image height to 200 pixel
$image->resize(height: 200);
```


### Resizing without exceeding the original size

> public Image::resizeDown(?int $width, ?int $height): ImageInterface

The method `resize()` simply stretches the image to the desired size. Use `resizeDown()` to change the size but do not exceed the original size of the image. The method support [named arguments](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments) to target just one axis for the modification. 


#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |


#### Examples

```php
use Intervention\Image\ImageManager;

// create new image instance (800 x 600)
$image = (new ImageManager('gd'))->make('images/example.jpg');

$image = $image->resizeDown(2000, 100); // 800 x 100

// resize only image width to 200 pixel and do not exceed the origial width
$image->resizeDown(width: 200);
```

## Scaling Images

### Resizing Images Proportionally

> public Image::scale(?int $width, ?int $height): ImageInterface

Often you want to resize an image but do not want to distort the original image aspect ratio. For this kind of modification you can simply use the methods `scale()` or `scaleDown()`.

Keep in mind that the resulting size my differ from the given arguments, because the aspect ratio will be maintained preferably.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |


#### Examples

```php
use Intervention\Image\ImageManager;

// create new image instance (800 x 600)
$image = (new ImageManager('gd'))->make('images/example.jpg');

// scale to fixed height
$image->scale(height: 300); // 400 x 300

// scale to 200 x 100 pixel
$image->scale(200, 100); // 200 x 150
```

### Scaling images but do not exceed the original size

> public Image::scaleDown(?int $width, ?int $height): ImageInterface

The method `resize()` simply stretches the image to the desired size. Use `resizeDown()` to change the size but do not exceed the original size of the image. The method support [named arguments](https://www.php.net/manual/en/functions.arguments.php#functions.named-arguments) to target just one axis for the modification. 


#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |


#### Examples

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = (new ImageManager('gd'))->make('images/example.jpg'); // 800 x 600

// scale down to fixed width
$image->scaleDown(width: 200); // 200 x 150

// scale down to fixed height
$image->scaleDown(height: 300); //  400 x 300
```

## Fitted Image Resizing

### Cropping & Resizing Combined

> public Image::fit(int $width, int $height, string $position = 'center'): ImageInterface

The `fit()` method is a two step combination of trimming excess pixels and resizing to achieve a certain result size. This method takes the given dimensions and scales it to the largest possible size matching the original size. Then this size is positioned on the original and cut out before being resized to the desired size from the arguments.

For this method both width and height arguments are required. You can optional set a position to determine where the image should be trimmed.

#### Parameters

| Name | Type | Description |
| - | - | - |
| width | integer | Desired image width. |
| height | integer | Desired image width. |
| position (optional) | string | Position |


#### Examples

```php
use Intervention\Image\ImageManager;

// create new image instance (800 x 600)
$image = (new ImageManager('gd'))->make('images/example.jpg');

// crop the best fitting 5:3 (600x360) ratio and resize to 600x360 pixel
$img->fit(600, 360);

// crop the best fitting 1:1 ratio (200x200) and resize to 200x200 pixel
$img->fit(200, 200);

// fit to 300x300 and position crop on the left
$image->fit(300, 300, 'left'); // 300 x 300 px
```

### Fitted resizing without exceeding the original size

> public Image::fitDown(int $width, int $height, string $position = 'center'): ImageInterface

This method has the same purpose and the same signature as `fit()` but the end result pixel size will never be larger than the original image. Use this if you want to prevent up-sampling your image.


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
$image = (new ImageManager('gd'))->make('images/example.jpg'); // 800 x 600

// fit down to 1200x720 (5:3)
$img->fitDown(1200, 720); // 800 x 480 (5:3)

// fit down to 900x900 (1:1)
$img->fitDown(900, 900); // 600 x 600

// fit down to 900x450 (2:1) and position left
$image->fitDown(900, 450, 'left'); // 800 x 400 px
```

## Padded Image Resizing

### Resizing & Padding Combined

> public Image::pad(int $width, int $height, $background = 'ffffff', string $position = 'center'): ImageInterface

Padded resizing means that the original image is scaled until it fits the defined target size with unchanged aspect ratio. Compared to the `fit()` method, this call does not create cropped areas, but new empty areas on the sides of the result image. These are filled with the specified background color.


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

// create new image instance
$image = (new ImageManager('gd'))->make('images/example.jpg');

// resize padded to 300 x 200
$image->pad(300, 200, 'ccc');

// resize padded with positioning
$image->pad(500, 500, position: 'top-left');
```

### Padded resizing without exceeding the original size

> public Image::padDown(int $width, int $height, $background = 'ffffff', string $position = 'center'): ImageInterface

This method does the same thing as `pad()` but does not exceed the size of the original image. You can use this if you want to prevent up-sampling.

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

// create new image instance (800 x 600)
$image = (new ImageManager('gd'))->make('images/example.jpg');

// resize padded without upsizing
$image->padDown(900, 600);

// padded resizing with background color
$image->padDown(500, 500, 'efefef');
```
