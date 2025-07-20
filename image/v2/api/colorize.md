---
label: "colorize()"
title: "Image::colorize"
subtitle: "Change the color balance of the current image"
sort: 7
---

> public Intervention\Image\Image colorize(integer $red, integer $green, integer $blue)

Change the RGB color values of the current image on the given channels **red**, **green** and **blue**. The input values are normalized so you have to include parameters from ```100``` for maximum color value ```0``` for no change and ```-100``` to take out all the certain color on the image.

### Parameters

#### red
Add or take out a amount of red color on the image. Use values between `-100` and `+100`.

#### green
Add or take out a amount of green color on the image. Use values between `-100` and `+100`.

#### blue
Add or take out a amount of blue color on the image. Use values between `-100` and `+100`.


### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// take out red color and add blue
$img->colorize(-100, 0, 100);

// just add a little green tone to the image
$img->colorize(0, 30, 0);
```

### See also

- [brightness](/v2/api/brightness)
- [contrast](/v2/api/contrast)
- [gamma](/v2/api/gamma)
- [greyscale](/v2/api/greyscale)
- [invert](/v2/api/invert)
- [pixelate](/v2/api/pixelate)
