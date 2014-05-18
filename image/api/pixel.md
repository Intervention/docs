# pixel — Draw a single pixel

## Description

> public Intervention\Image\Image pixel( mixed $color, integer $x, integer $y )

Draw a single pixel in given **color** on **x, y position**.


## Parameters

### color
The color of the pixel. Pass a color in one of the different [color formats](/getting_started/formats).

### x
x-coordinate of the pixel.

### y
y-coordinate of the pixel.

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create empty canvas with background color
$img = Image::canvas(100, 100, '#ddd');

// draw a blue pixel
$img->pixel('#0000ff', 32, 32);

// draw a red pixel
$img->pixel('#ff0000', 64, 64);
```


## See also

- [line](/api/line)
- [rectangle](/api/rectangle)
- [circle](/api/circle)
- [ellipse](/api/ellipse)
