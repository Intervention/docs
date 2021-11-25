# gamma()
## Apply gamma correction to the current image

> public Intervention\Image\Image gamma(float $correction)

Apply a gamma correction operation on the current image.

### Parameters

#### correction
Gamma compensation value.

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// apply gamma correction
$img->gamma(1.6);
```

### See also

- [brightness](/v2/api/brightness)
- [contrast](/v2/api/contrast)
- [colorize](/v2/api/colorize)
- [greyscale](/v2/api/greyscale)
- [invert](/v2/api/invert)
- [pixelate](/v2/api/pixelate)
