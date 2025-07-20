---
label: "brightness()"
title: "Image::brightness"
subtitle: "Change the brightness of an image"
sort: 3
---

> public Intervention\Image\Image brightness(integer $level)

Changes the brightness of the current image by the given **level**. Use values between ```-100``` for min. brightness ```0``` for no change and ```+100``` for max. brightness.

### Parameters

#### level
Level of brightness change applied to the current image. Use values between `-100` and `+100`.

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// increase brightness of image
$img->brightness(35);
```

### See also

- [contrast](/v2/api/contrast)
- [gamma](/v2/api/gamma)
- [colorize](/v2/api/colorize)
- [greyscale](/v2/api/greyscale)
- [invert](/v2/api/invert)
- [pixelate](/v2/api/pixelate)
