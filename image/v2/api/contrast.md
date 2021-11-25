# contrast()
## Change the color contrast of the current image

> public Intervention\Image\Image contrast(integer $level)

Changes the contrast of the current image by the given **level**. Use values between ```-100``` for min. contrast ```0``` for no change and ```+100``` for max. contrast.

### Parameters

#### level
Level of contrast change applied to the current image. Use values between `-100` and `+100`.

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// increase brightness of image
$img->contrast(65);
```

### See also

- [brightness](/v2/api/brightness)
- [gamma](/v2/api/gamma)
- [colorize](/v2/api/colorize)
- [greyscale](/v2/api/greyscale)
- [invert](/v2/api/invert)
- [pixelate](/v2/api/pixelate)