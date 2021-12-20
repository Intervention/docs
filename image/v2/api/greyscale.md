# Image::greyscale
## Turn the current image into a greyscale version

> public Intervention\Image\Image greyscale()

Turns image into a greyscale version.

### Parameters

none

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create new Intervention Image and turn it into greyscale version
$img = Image::make('public/foo.jpg')->greyscale();
```

### See also

- [brightness](/v2/api/brightness)
- [contrast](/v2/api/contrast)
- [colorize](/v2/api/colorize)
- [invert](/v2/api/invert)
- [pixelate](/v2/api/pixelate)
