# Image::invert
## Invert the colors of the current image

> public Intervention\Image\Image invert()

Invert all colors of the current image.

### Parameters

none

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create Image from file and reverse colors
$img = Image::make('public/foo.jpg')->invert();
```

### See also

- [brightness](/v2/api/brightness)
- [contrast](/v2/api/contrast)
