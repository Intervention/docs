# Image::resizeCanvas
## Resize the current image boundaries

> public Intervention\Image\Image resizeCanvas (int $width, int $height, [string $anchor, [boolean $relative, [mixed $bgcolor]]])

Resize the boundaries of the current image to given **width and height**. An **anchor** can be defined to determine from what point of the image the resizing is going to happen. Set the mode to **relative** to add or subtract the given width or height to the actual image dimensions. You can also pass a **background color** for the emerging area of the image.

### Parameters

#### width
The new width in pixels of the image in absolute mode or the amount of pixels to add or subtract from height in relative mode.

#### height
The new height in pixels of the image in absolute mode or the amount of pixels to add or subtract from height in relative mode.

#### anchor (optional)
Set a point from where the image resizing is going to happen. For example if you are setting the anchor to ```bottom-left``` this side is pinned and the values of width/height will be added or subtracted to the top-right corner of the image.

The possible values for this parameter are:

- `top-left`
- `top`
- `top-right`
- `left`
- `center` (default)
- `right`
- `bottom-left`
- `bottom`
- `bottom-right`


#### relative (optional)
Determine that the resizing is going to happen in relative mode. Meaning that the values of width or height will be added or substracted from the current height of the image. Default: `false`

#### bgcolor (optional)
A background color for the new areas of the image. The background color can be passed in different [color formats](/getting_started/formats). Default: `#ffffff`, transparent if supported by the output format

### Return Values
Resized instance of `Intervention\Image\Image`

### Examples

```php
// create Image from file
$img = Image::make('public/foo.jpg');

// resize image canvas
$img->resizeCanvas(300, 200);

// resize only the width of the canvas
$img->resizeCanvas(300, null);

// resize only the height of the canvas
$img->resizeCanvas(null, 200);

// resize the canvas by cutting out bottom right position
$img->resizeCanvas(300, 200, 'bottom-right');

// resize the canvas relative by setting the third parameter to true
$img->resizeCanvas(10, -10, 'center', true);

// set a background-color for the emerging area
$img->resizeCanvas(1280, 720, 'center', false, 'ff00ff');
```

### See also

- [resize](/v2/api/resize)
- [fit](/v2/api/fit)
- [crop](/v2/api/crop)
- [trim](/v2/api/trim)
