---
title: "Drawing"
subtitle: "Draw Geometric Shapes on Images"
lead: "Learn how to draw shapes and customize images with Intervention Image. Add colors, pixels, rectangles, circles, polygons, and bézier curves using a simple interface for precise and intuitive control."
sort: 4
---

[TOC]

## Colors & Pixels

### Fill Images with Color

> public Image::fill(mixed $color, null|int $x = null, null|int $y = null): ImageInterface

Fills the current image with the specified color. Optionally, it is possible to
pass a position where the color fill should start. If these X and Y values are
specified, the color will be applied with flood fill. This means that only
colors that are at the specified position will be filled. If no position is
passed, the entire image will be filled.

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | mixed | Fill color in one of the different [color formats](/v3/getting-started/formats#color-formats) |
| x | int | Optional x-coordinate of the filling position |
| y | int | Optional y-coordinate of the filling position |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// read an image
$image = $manager->read('images/example.png');

// flood fill image with color
$image = $image->fill('#b53717', 10, 10);
```

### Draw Pixels

> public Image::drawPixel(int $x, int $y, mixed $color): ImageInterface

Draw a single pixel at the specified position defined by the coordinates **x** and **y** in a given **color**.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | integer | Position of pixel on x-axis of the current image |
| y | integer | Position of pixel on y-axis of the current image |
| color | mixed | Color of the pixel in a [valid format](/v3/getting-started/formats#color-formats) |


#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create an test image from a file
$manager = new ImageManager(new Driver());
$image = $manager->read('test.png');

// draw three pixels at different positions
$image->drawPixel(12, 30, 'ff00ff');
$image->drawPixel(100, 1, 'rgb(255, 255, 0)');
$image->drawPixel(200, 2, 'orange');
```


## Geometric Shapes

### Draw a Rectangle

> public Image::drawRectangle(int $x, int $y, Closure|Rectangle $init): ImageInterface

Draw a colored rectangle on the current image with its top left position at the
**x, y** coordinates. Define the overall appearance of the shape by passing an
**init** callback or a rectangle object as a third parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | integer | Position of the top left corner of the rectangle on x-axis of the current image |
| y | integer | Position of the top left corner of the rectangle on y-axis of the current image |
| init | Closure or Intervention\Image\Geometry\Rectangle | Callback to define the appearance of the rectangle or Rectangle object. See example. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\RectangleFactory;

// create an test image from a file
$manager = new ImageManager(new Driver());
$image = $manager->read('test.png');

// draw an orange rectangle with a border
$image->drawRectangle(10, 10, function (RectangleFactory $rectangle) {
    $rectangle->size(180, 125); // width & height of rectangle
    $rectangle->background('orange'); // background color of rectangle
    $rectangle->border('white', 2); // border color & size of rectangle
});
```

### Draw Ellipses

> public Image::drawEllipse(int $x, int $y, Closure|Ellipse $init): ImageInterface

Draw a colored ellipse on the current image with its center position at the
**x, y** coordinates. Define the overall appearance of the shape by passing a
**init** callback or a ellipse objeect as a third parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | integer | Position of the center of the ellipse on x-axis of the current image |
| y | integer | Position of the center of the ellipse on y-axis of the current image |
| init | Closure or Intervention\Image\Geometry\Ellipse | Callback to define the appearance of the ellipse or Ellipse object. See example. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Geometry\Factories\EllipseFactory;

// create an test image from a file
$manager = new ImageManager(Driver::class);
$image = $manager->read('test.png');

// draw a red ellipse with a blue border
$image->drawEllipse(10, 10, function (EllipseFactory $ellipse) {
    $ellipse->size(180, 125); // width & height of ellipse
    $ellipse->background('f00'); // background color
    $ellipse->border('00f', 1); // border color & size
});
```

### Draw a Circle

> public Image::drawCircle(int $x, int $y, Closure|Circle $init): ImageInterface

Draw a colored circle on the current image with its center position at the **x,
y** coordinates. Define the overall appearance of the shape by passing a
**init** callback or a circle object as a third parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | integer | Position of the center of the circle on x-axis of the current image |
| y | integer | Position of the center of the circle on y-axis of the current image |
| init | Closure or Intervention\Image\Geometry\Circle | Callback to define the appearance of the circle or object. See example. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\CircleFactory;

// create an test image from a file
$manager = new ImageManager(Driver::class);
$image = $manager->read('test.png');

// draw a green circle with a white border
$image->drawCircle(10, 10, function (CircleFactory $circle) {
    $circle->radius(150); // radius of circle in pixels
    $circle->background('lightblue'); // background color
    $circle->border('b53717', 1); // border color & size
});
```

### Draw a Line

> public Image::drawLine(Closure|Line $init): ImageInterface

Draw a line on the current image. Define the overall appearance of the shape by
passing a **init** callback or a line object.

#### Parameters

| Name | Type | Description |
| - | - | - |
| init | Closure or Intervention\Image\Geometry\Line | Callback to define the appearance of the line or line object. See example. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\LineFactory;

// create an test image from a file
$manager = new ImageManager(Driver::class);
$image = $manager->read('test.png');

// draw a half transparent white line
$image->drawLine(function (LineFactory $line) {
    $line->from(10, 10); // starting point of line
    $line->to(300, 100); // ending point
    $line->color('ff00ff'); // color of line
    $line->width(5); // line width in pixels
});
```

### Draw a Polygon

> public Image::drawPolygon(Closure|Polygon $init): ImageInterface

Draw a polygon on the current image. Define the overall appearance of the shape
by passing a **init** callback or a polygon object.

#### Parameters

| Name | Type | Description |
| - | - | - |
| init | Closure or Intervention\Image\Geometry\Polygon | Callback to define the appearance of the polygon or polygon object. See example. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Geometry\Factories\PolygonFactory;

// create an test image from a file
$manager = new ImageManager(new Driver());
$image = $manager->read('test.png');

// draw a polygon
$image->drawPolygon(function (PolygonFactory $polygon) {
    $polygon->point(10, 10); // add point of polygon
    $polygon->point(150, 150); // add point
    $polygon->point(40, 180); // add point
    $polygon->point(60, 100); // add point
    $polygon->background('#b35187'); // background color
    $polygon->border('#ff0', 6); // border color and border width
});
```

### Draw Bezier Curves

> public Image::drawBezier(Closure|Bezier $init): ImageInterface

This method draws [Bézier curves](https://en.wikipedia.org/wiki/B%C3%A9zier_curve), the 
shape of which is defined by a set of control points specified in the callback.
The type of curve drawn depends on the number of control points specified, 
which must be either three or four. With three control points, the result is a 
**quadratic Bézier curve**, while four points result in a **cubic Bézier curve**. The 
first and last control points define the start and end points of the curve.

The color, width and background color of the curve can also be set using the callback.

#### Parameters

| Name | Type | Description |
| - | - | - |
| init | Closure or Intervention\Image\Geometry\Bezier | Callback to define the appearance and position of the bézier curve or object. See example. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Geometry\Factories\BezierFactory;

// create a new image
$image = ImageManager::gd()
    ->create(500, 500)
    ->fill('666');

// draw a yellow quadratic bezier curve with a filled red background
$image->drawBezier(function (BezierFactory $bezier) {
    $bezier->point(300, 260); // control point 1
    $bezier->point(150, 335); // control point 2
    $bezier->point(300, 410); // control point 3
    $bezier->background('f00'); // background color
    $bezier->border('ff0'); // border color
});

// draw a 4px red cubic bezier curve with four control points
$image->drawBezier(function (BezierFactory $bezier) {
    $bezier->point(50, 50); // control point 1
    $bezier->point(200, 50); // control point 2
    $bezier->point(150, 200); // control point 3
    $bezier->point(300, 200); // control point 4
    $bezier->border('ff0000', 4); // border color & size
});
```
