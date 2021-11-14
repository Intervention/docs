# crop — Crop an image

## Description

> public Intervention\Image\Image crop(int $width, int $height, [int $x, int $y])

Cut out a rectangular part of the current image with given **width and height**. Define optional **x,y coordinates** to move the top-left corner of the cutout to a certain position.


## Parameters

### width
Width of the rectangular cutout.

### height
Height of the rectangular cutout.

### x (optional)
X-Coordinate of the top-left corner if the rectangular cutout. By default the rectangular part will be centered on the current image.

### y (optional)
Y-Coordinate of the top-left corner if the rectangular cutout. By default the rectangular part will be centered on the current image.

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// open file a image resource
$img = Image::make('public/foo.jpg');

// crop image
$img->crop(100, 100, 25, 25);
```


## See also

- [resize](/api/resize)
- [resizeCanvas](/api/resizeCanvas)
- [fit](/api/fit)
- [trim](/api/trim)
