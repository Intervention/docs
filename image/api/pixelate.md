# pixelate — Pixelate an image

## Description

> public Intervention\Image\Image pixelate(integer $size)

Applies a pixelation effect to the current image with a given **size** of pixels.

## Parameters

### size
Size of the pixels.

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// apply pixelation effect
$img->pixelate(12);
```

## See also

- [brightness](/api/brightness)
- [contrast](/api/contrast)
- [greyscale](/api/greyscale)
- [invert](/api/invert)
