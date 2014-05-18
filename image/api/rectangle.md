# rectangle — draw a rectangle

## Description

> public Intervention\Image\Image rectangle( int $x1, int $y1, int $x2, int $y2, [Closure $callback])

Draw a colored rectangle on current image with top-left corner on **x,y point 1** and bottom-right corner at **x,y point 2**. Define the overall appearance of the shape by passing a Closure **callback** as an optional parameter.


## Parameters

### x1
x-coordinate of the top-left point of the rectangle.

### y1
y-coordinate of the top-left point of the rectangle.

### x2
x-coordinate of the bottom-right point of the rectangle.

### y2
y-coordinate of the bottom-right point of the rectangle.

### callback (optional)
Define the appearance of the rectangle.


## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create empty canvas with background color
$img = Image::canvas(100, 100, '#ddd');

// draw an empty rectangle border
$img->rectangle(10, 10, 190, 190);

// draw filled red rectangle
$img->rectangle(5, 5, 195, 195, function ($draw) {
    $draw->background('#ff0000');
});

// draw transparent rectangle with 2px border
$img->rectangle(5, 5, 195, 195, function ($draw) {
    $draw->background('rgba(255, 255, 255, 0.5)');
    $draw->border(2, '#000');
});
```

## See also

- [pixel](/api/pixel)
- [line](/api/line)
- [circle](/api/circle)
- [ellipse](/api/ellipse)
