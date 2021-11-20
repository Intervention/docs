> public Intervention\Image\Image blur([integer $amount])

**Note: Performance intensive on larger amounts of blur with GD driver. Use with care.**

## Parameters

### amount (optional)
The amount of the blur strength. Use values between `0` and `100`. Default: `1`

## Return Values
Instance of `Intervention\Image\Image`

## Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// apply slight blur filter
$img->blur();

// apply stronger blur
$img->blur(15);
```

## See also

- [sharpen](/api/sharpen)
- [pixelate](/api/pixelate)
- [brightness](/api/brightness)
- [contrast](/api/contrast)
