> public Intervention\Image\Image line(int $x1, int $y1, int $x2, int $y2, [Closure $callback])

Draw a line from **x,y point 1** to **x,y point 2** on current image. Define **color and/or width** of line in an optional Closure callback.

## Parameters

### x1
X-Coordinate of the starting point.

### y1
Y-Coordinate of the starting point.

### x2
X-Coordinate of the end point.

### y2
Y-Coordinate of the end point.

### callback
Define appearance of line. See examples below. Use the following methods to pass details.

#### color

> public Intervention\Image\AbstractShape color(string $color)

Set color of the line in one of the available [color formats](/getting_started/formats). Default: `#000000`

#### width

> public Intervention\Image\AbstractShape width(integer $width)

Set the width of the line in pixels. **Option is not available with GD driver** Default: `1`


## Return Values
Instance of `Intervention\Image\Image`

## Examples

```php
// create empty canvas with background color
$img = Image::canvas(100, 100, '#ddd');

// draw a blue line
$img->line(10, 10, 100, 10, function ($draw) {
    $draw->color('#0000ff');
});

// draw a red line with 5 pixel width
$img->line(10, 10, 195, 195, function ($draw) {
    $draw->color('#f00');
    $draw->width(5);
});
```

## See also

- [pixel](/api/pixel)
- [rectangle](/api/rectangle)
- [circle](/api/circle)
- [ellipse](/api/ellipse)
- [polygon](/api/polygon)
