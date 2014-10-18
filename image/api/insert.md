# insert — Paste over another image

## Description

> public Intervention\Image\Image insert(mixed $source, [string $position, [integer $x, integer $y]])

Paste a given **image source** over the current image with an optional **position** and a **offset coordinate**. This method can be used to apply another image as watermark because the transparency values are maintained.


## Parameters

### source
The image source that will inserted on top of the current image. The method can handle the following types of input:

- **string** - Path of the image in filesystem.
- **string** - URL of an image (```allow_url_fopen``` must be enabled).
- **string** - Binary image data.
- **string** - Data-URL encoded image data.
- **string** - Base64 encoded image data.
- **resource** - PHP resource of type gd.
- **object** - Imagick instance
- **object** - Intervention\Image\Image instance
- **object** - SplFileInfo instance (To handle Laravel file uploads via Symfony\Component\HttpFoundation\File\UploadedFile)

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

### x (optional)
Optional relative offset of the new image on x-axis of the current image. Offset will be calculated relative to the position parameter. Default: 0

### y (optional)
Optional relative offset of the new image on y-axis of the current image. Offset will be calculated relative to the position parameter. Default: 0

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
$img->insert('public/watermark.png', 'bottom-right', 10, 10);
```

See also

- [mask](/api/mask)

