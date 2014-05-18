# blur — Blurs an image

## Description

> public Intervention\Image\Image blur( [integer $amount] )

Apply a gaussian blur filter with a certain **amount** on the current image.

**Note: Performance intensive on larger amounts of blur with GD driver. Use with care.**

## Parameters

### amount (optional)
The amount of the blur strength. Usually values between 1 and 10 will do the work in acceptable time. Default: 1

## Return Values
Instance of Intervention\Image\Image

Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// apply slight blur filter
$img->blur(1);

// apply stronger blur
$img->blur(15);
```

## See also

- [pixelate](/api/pixelate)
- [brightness](/api/brightness)
- [contrast](/api/contrast)