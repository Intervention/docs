# circle — Draw a circle

## Description

> public Intervention\Image\Image circle( integer $radius, integer $x, integer $y, [Closure $callback] )

Draw a circle at given **x, y, coordinates** with given **radius**. You can define the **appearance** of the circle by an optional closure callback.


## Parameters

### radius
radius of the circle in pixels.

### pos_x
x-coordinate of the center.

### pos_y
y-coordinate of the center.

### callback (optional)
Define appearance of circle. See examples below. Use the following methods to pass details.

#### background

> public Intervention\Image\AbstractShape background( string $color )

Define the background-color of the circle in one of the available [color formats](/getting_started/formats).

#### border

> public Intervention\Image\AbstractShape border( integer $width, string $color )

Define the border of the circle. Set width as pixels in the first and the border-color in one of the available [color formats](/getting_started/formats) as second parameter.


## Return Values
Instance of Intervention\Image\Image

##Examples

```php
// create empty canvas with background color
$img = Image::canvas(300, 200, '#ddd');

// draw a filled blue circle
$img->circle(100, 50, 50, function ($draw) {
    $draw->background('#0000ff');
});

// draw a filled blue circle with red border
$img->circle(10, 100, 100, function ($draw) {
    $draw->background('#0000ff');
    $draw->border(1, '#f00');
});

// draw an empty circle with 5px border
$img->circle(70, 150, 100, function ($draw) {
    $draw->border(5, '000000');
});
```


## See also

- [pixel](/api/pixel)
- [line](/api/line)
- [rectangle](/api/rectangle)
- [ellipse](/api/ellipse)
- [polygon](/api/polygon)
