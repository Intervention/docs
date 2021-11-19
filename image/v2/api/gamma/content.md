## Description

> public Intervention\Image\Image gamma( float $correction )

Performs a gamma correction operation on the current image.


## Parameters

### correction
Gamma compensation value.


## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// apply gamma correction
$img->gamma(1.6);
```

## See also

- [brightness](/api/brightness)
- [contrast](/api/contrast)
- [colorize](/api/colorize)
- [greyscale](/api/greyscale)
- [invert](/api/invert)
- [pixelate](/api/pixelate)
