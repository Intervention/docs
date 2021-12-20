# Image::polygon
## Draw a polygon to the current image

> public Intervention\Image\Image polygon(array $points, [Closure $callback])

Draw a **colored** polygon with given **points**. You can define the **appearance** of the polygon by an optional closure callback.

### Parameters

#### points
Points of the polygon defined by a single-dimensional array alternating x, y points. **See examples below.**

#### callback (optional)
Define appearance of polygon. Use the following methods to pass details.

> public Intervention\Image\AbstractShape background(string $color)

Define the background-color of the polygon in one of the available [color formats](/getting_started/formats).

> public Intervention\Image\AbstractShape border(integer $width, string $color)

Define the border of the polygon. Set width as pixels in the first and the border-color in one of the available [color formats](/getting_started/formats) as second parameter.

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create empty canvas with background color
$img = Image::canvas(800, 600, '#ddd');

// define polygon points
$points = [
    40,  50,  // Point 1 (x, y)
    20,  240, // Point 2 (x, y)
    60,  60,  // Point 3 (x, y)
    240, 20,  // Point 4 (x, y)
    50,  40,  // Point 5 (x, y)
    10,  10   // Point 6 (x, y)
];

// draw a filled blue polygon with red border
$img->polygon($points, function ($draw) {
    $draw->background('#0000ff');
    $draw->border(1, '#ff0000');
});
```

### See also

- [pixel](/v2/api/pixel)
- [line](/v2/api/line)
- [rectangle](/v2/api/rectangle)
- [circle](/v2/api/circle)
- [ellipse](/v2/api/ellipse)
