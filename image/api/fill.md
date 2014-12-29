# fill — fill image with color or pattern

## Description

> public Intervention\Image\Image fill(mixed $filling, [integer $x, integer $y])

Fill current image with given **color** or another **image** used as tile for filling. Pass optional **x, y coordinates** to start at a certain point.

If a certain position is defined, the color at that point on the original image is used to perform a flood fill. If no x,y coordinates are passed, the whole picture is filled no matter what is beneath.


## Parameters

### filling
The fill color or image pattern. Pass a **color** as one of the different [color formats](/getting_started/formats) or to fill the image with tiles an image resource in the following formats:

- **string** - Path of the image in filesystem.
- **string** - URL of an image (```allow_url_fopen``` must be enabled).
- **string** - Binary image data.
- **string** - Data-URL encoded image data.
- **string** - Base64 encoded image data.
- **resource** - PHP resource of type gd. (when using GD driver)
- **object** - Imagick instance (when using Imagick driver)
- **object** - Intervention\Image\Image instance
- **object** - SplFileInfo instance (To handle Laravel file uploads via Symfony\Component\HttpFoundation\File\UploadedFile)

### x (optional)
Starting point on x-axis for the filling.

### y (optional)
Starting point on y-axis for the filling.

**If a x, y coordinate is defined the filling will be flood filled based on the color at this position.**


## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create empty canvas
$img = Image::canvas(800, 600);

// fill image with color
$img->fill('#cccccc');

// fill image with tiled image
$img->fill('tile.png');

// flood fill image with color
$img->fill('#ff00ff', 0, 0);
```

## See also

- [pixel](/api/pixel)
