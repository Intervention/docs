# Image::pixelate
## Apply pixelation filter to the current image

> public Intervention\Image\Image pixelate(integer $size)

Applies a pixelation effect to the current image with a given **size** of pixels.

### Parameters

#### size
Size of the pixels.

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// apply pixelation effect
$img->pixelate(12);
```

### See also

- [brightness](/v2/api/brightness)
- [contrast](/v2/api/contrast)
- [greyscale](/v2/api/greyscale)
- [invert](/v2/api/invert)
