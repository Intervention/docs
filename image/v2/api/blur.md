# blur
## Apply a gaussian blur filter with a optional amount on the current image.

> public Intervention\Image\Image blur([integer $amount])

**Note: Performance intensive on larger amounts of blur with GD driver. Use with care.**

### Parameters

#### amount (optional)
The amount of the blur strength. Use values between `0` and `100`. Default: `1`

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// apply slight blur filter
$img->blur();

// apply stronger blur
$img->blur(15);
```

### See also

- [sharpen](/v2/api/sharpen)
- [pixelate](/v2/api/pixelate)
- [brightness](/v2/api/brightness)
- [contrast](/v2/api/contrast)
