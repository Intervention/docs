## Description

> public Intervention\Image\Image contrast(integer $level)

Changes the contrast of the current image by the given **level**. Use values between ```-100``` for min. contrast ```0``` for no change and ```+100``` for max. contrast.


## Parameters

### level
Level of contrast change applied to the current image. Use values between -100 and +100.

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// increase brightness of image
$img->contrast(65);
```

## See also

- [brightness](/api/brightness)
- [gamma](/api/gamma)
- [colorize](/api/colorize)
- [greyscale](/api/greyscale)
- [invert](/api/invert)
- [pixelate](/api/pixelate)