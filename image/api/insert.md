# insert — Paste over another image

## Description

> public Intervention\Image\Image insert(mixed $source [, integer $x, integer $y, string $position])

Paste a given **image source** over the current image with an optional **position** and a **offset coordinate**. This method can be used to apply another image as watermark because the transparency values are maintained.


## Parameters

### source
The image source that will inserted on top of the current image. The method can handle the following types of input:

- **string** - Path of the image in filesystem.
- **string** - Binary image data.
- **resource** - PHP resource of type gd.
- **object** - Instance of Imagick
- **object** - Instance of Intervention\Image\Image

### x (optional)
Optional relative offset of the new image on x-axis of the current image. Offset will be calculated relative to the position parameter. Default: 0

### y (optional)
Optional relative offset of the new image on y-axis of the current image. Offset will be calculated relative to the position parameter. Default: 0

### position (optional)
Set a position where image will be inserted. For example if you are setting the anchor to ```bottom-left``` the image will be positioned at the bottom-left border of the current image. The position of the new image will be calculated relatively to this location.

The possible values are:

- top-left (default)
- top
- top-right
- left
- center
- right
- bottom-left
- bottom
- bottom-right
- 
## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// paste another image
$img->insert('public/bar.png');

// create a new Image instance for inserting
$watermark = Image::make('public/watermark.png');
$img->insert($watermark, 'center');

// insert watermark at bottom-right corner with 10px offset
$img->insert('public/watermark.png', 10, 10, 'bottom-right');
```

See also

- [mask](/api/mask)

