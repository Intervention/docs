# ellipse — Draw an ellipse

## Description

> public Intervention\Image\Image ellipse(int $width, int $height, int $x, int $y, [Closure $callback])

Draw a **colored** ellipse at given **x, y, coordinates**. You can define **width** and **height** and set the **appearance** of the circle by an optional closure callback.

## Parameters

### width
width of the ellipse. Default: 10

### height
The ellipse height. Default: 10

### x
x-coordinate of the center.

### y
y-coordinate of the center.

### callback (optional)
Define the appearance of the circle. See examples for usage.

## Return Values
Instance of Intervention\Image\Image

## Examples

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


## See also

- [pixel](/api/pixel)
- [line](/api/line)
- [rectangle](/api/rectangle)
- [circle](/api/circle)
