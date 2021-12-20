# Image::ellipse
## Draw an ellipse to the current image

> public Intervention\Image\Image ellipse(int $width, int $height, int $x, int $y, [Closure $callback])

Draw a **colored** ellipse at given **x, y, coordinates**. You can define **width** and **height** and set the **appearance** of the circle by an optional closure callback.

### Parameters

#### width
width of the ellipse. Default: `10`

#### height
The ellipse height. Default: `10`

#### x
x-coordinate of the center.

#### y
y-coordinate of the center.

#### callback (optional)
Define appearance of ellipse. See examples below. Use the following methods to pass details.

> public Intervention\Image\AbstractShape background(string $color)

Define the background-color of the ellipse in one of the available [color formats](/getting_started/formats).

> public Intervention\Image\AbstractShape border(integer $width, string $color)

Define the border of the ellipse. Set width as pixels in the first and the border-color in one of the available [color formats](/getting_started/formats) as second parameter.

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create empty canvas with background color
$img = Image::canvas(800, 600, '#ddd');

// draw a filled blue ellipse
$img->ellipse(25, 30, 50, 50, function ($draw) {
    $draw->background('#0000ff');
});

// draw a filled blue ellipse with red border
$img->ellipse(60, 120, 100, 100, function ($draw) {
    $draw->background('#0000ff');
    $draw->border(1, '#ff0000');
});

// draw an empty ellipse with a 5px border
$img->ellipse(150, 200, 300, 200, function ($draw) {
    $draw->border(5, 'fff');
});
```


### See also

- [pixel](/v2/api/pixel)
- [line](/v2/api/line)
- [rectangle](/v2/api/rectangle)
- [circle](/v2/api/circle)
- [polygon](/v2/api/polygon)
