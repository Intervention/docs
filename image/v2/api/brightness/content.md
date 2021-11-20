> public Intervention\Image\Image brightness(integer $level)

Changes the brightness of the current image by the given **level**. Use values between ```-100``` for min. brightness ```0``` for no change and ```+100``` for max. brightness.

## Parameters

### level
Level of brightness change applied to the current image. Use values between `-100` and `+100`.

## Return Values
Instance of `Intervention\Image\Image`

## Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// increase brightness of image
$img->brightness(35);
```

## See also

- [contrast](/api/contrast)
- [gamma](/api/gamma)
- [colorize](/api/colorize)
- [greyscale](/api/greyscale)
- [invert](/api/invert)
- [pixelate](/api/pixelate)