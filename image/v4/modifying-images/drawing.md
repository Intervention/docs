---
title: "Drawing"
subtitle: "Draw Geometric Shapes on Images"
lead: "Learn how to draw shapes and customize images with Intervention Image. Add colors, pixels, rectangles, circles, polygons, and bézier curves using a simple interface for precise and intuitive control."
sort: 4
---

[TOC]

## Colors & Pixels

### Fill Images with Color

> public Image::fill(string|ColorInterface $color, null|int $x = null, null|int $y = null): ImageInterface

Fills the current image with the specified color. Optionally, it is possible to
pass a position where the color fill should start. If these X and Y values are
specified, the color will be applied with flood fill. This means that only
colors that are at the specified position will be filled. If no position is
passed, the entire image will be filled.

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | string or ColorInterface | Fill color in one of the different [color formats](/v4/getting-started/formats#color-formats) |
| x | int | Optional x-coordinate of the filling position |
| y | int | Optional y-coordinate of the filling position |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = ImageManager::usingDriver(Driver::class);

// read an image
$image = $manager->read('images/example.png');

// flood fill image with color
$image = $image->fill('#b53717', 10, 10);
```

### Draw Pixels

> public Image::drawPixel(int $x, int $y, string|ColorInterface $color): ImageInterface

Draw a single pixel at the specified position defined by the coordinates **x** and **y** in a given **color**.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | integer | Position of pixel on x-axis of the current image |
| y | integer | Position of pixel on y-axis of the current image |
| color | string or ColorInterface | Color of the pixel in a [valid format](/v4/getting-started/formats#color-formats) |


#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;
use Intervention\Image\Color;
use Intervention\Image\Colors\NamedColor;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// draw pixels at different positions
$image->drawPixel(200, 2, Color::rgb(255, 55, 0, .2));
$image->drawPixel(12, 30, 'ff00ff');
$image->drawPixel(100, 1, 'rgb(255, 255, 0)');
$image->drawPixel(200, 2, 'orange');
$image->drawPixel(200, 2, NamedColor::STEELBLUE);
```


## Geometric Shapes

### Draw a Rectangle

> public Image::drawRectangle(callable|Rectangle $rectangle, null|callable $adjustments = null): ImageInterface

Draw a rectangle on the current image. Define the overall appearance of the
shape by passing an callback or a rectangle object. Optionally you can pass an
adjustment callback to modify the given rectangle for this single call.

#### Parameters

| Name | Type | Description |
| - | - | - |
| rectangle | callable or Intervention\Image\Geometry\Rectangle | The rectangle or a callback on a rectangle factory. See example. |
| adjustments | null or callable | A callable to adjust the appearance of the given rectangle for this drawing operation. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\RectangleFactory;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// draw an orange rectangle with a border
$image->drawRectangle(function (RectangleFactory $rectangle): void {
    $rectangle->at(10, 10); // position of the rectangle on the image
    $rectangle->size(180, 125); // width & height of rectangle
    $rectangle->background('ff5500'); // background color of rectangle
    $rectangle->border('white', 2); // border color & size of rectangle
});
```

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\RectangleFactory;
use Intervention\Image\Geometry\Factories\Drawable;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

$background = Color::rgb(255, 55, 0);

// create rectangle object to reuse in following calls
$rectangle = Drawable::rectangle(function (RectangleFactory $rectangle) use ($background): void {
     $rectangle->size(32, 32);
     $rectangle->background($background->withTransparency(.7));
 });

// draw rectangle object at position
$image->drawRectangle($rectangle, fn($rectangle) => $rectangle->at(10, 10));

// draw rectangle object at new position
$image->drawRectangle($rectangle, fn($rectangle) => $rectangle->at(100, 100));

// draw rectangle object at another position
$image->drawRectangle($rectangle, fn($rectangle) => $rectangle->at(200, 200));
```

### Draw Ellipses

> public Image::drawEllipse(callable|Ellipse $ellipse, null|callable $adjustments = null): ImageInterface

Draw a ellipse on the current image. Define the overall appearance of the
shape by passing an callback or a ellipse object. Optionally you can pass an
adjustment callback to modify the given geometric object for this single call.

#### Parameters

| Name | Type | Description |
| - | - | - |
| ellipse | callable or Intervention\Image\Geometry\Ellipse | The ellipse or a callback on a ellipse factory. See example. |
| adjustments | null or callable | A callable to adjust the appearance of the given ellipse for this drawing operation. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\EllipseFactory;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// draw an ellipse with a border
$image->drawEllipse(function (EllipseFactory $ellipse): void {
    $ellipse->at(10, 10); // position of the ellipse on the image
    $ellipse->size(180, 125); // width & height of ellipse
    $ellipse->background('ff5500'); // background color of ellipse
    $ellipse->border('white', 2); // border color & size of ellipse
});
```

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\EllipseFactory;
use Intervention\Image\Geometry\Factories\Drawable;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// create background color for the ellipse
$background = Color::rgb(255, 55, 0);

// create ellipse object to reuse in following calls
$ellipse = Drawable::ellipse(function (EllipseFactory $ellipse) use ($background): void {
     $ellipse->width(100);
     $ellipse->height(200);
     $ellipse->background($background->withTransparency(.7));
 });

// draw ellipse object at position
$image->drawEllipse($ellipse, fn($ellipse) => $ellipse->at(10, 10));

// draw ellipse object at new position
$image->drawEllipse($ellipse, fn($ellipse) => $ellipse->at(100, 100));

// draw ellipse object at another position
$image->drawEllipse($ellipse, fn($ellipse) => $ellipse->at(200, 200));
```

### Draw a Circle

> public Image::drawCircle(callable|Circle $circle, null|callable $adjustments = null): ImageInterface

Draw a circle on the current image. Define the overall appearance of the
shape by passing an callback or a circle object. Optionally you can pass an
adjustment callback to modify the given geometric object for this single call.

#### Parameters

| Name | Type | Description |
| - | - | - |
| circle | callable or Intervention\Image\Geometry\Circle | The circle or a callback on a circle factory. See example. |
| adjustments | null or callable | A callable to adjust the appearance of the given circle for this drawing operation. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\CircleFactory;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// draw an circle with a border
$image->drawCircle(function (CircleFactory $circle): void {
    $circle->at(10, 10); // position of the circle on the image
    $circle->diameter(180); // diameter of circle
    $circle->background('ff5500'); // background color of circle
    $circle->border('white', 2); // border color & size of circle
});
```

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\CircleFactory;
use Intervention\Image\Geometry\Factories\Drawable;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// create background color for the circle
$background = Color::rgb(255, 55, 0);

// create circle object to reuse in following calls
$circle = Drawable::circle(function (CircleFactory $circle) use ($background): void {
     $circle->diameter(100);
     $circle->background($background->withTransparency(.7));
 });

// draw circle object at position
$image->drawCircle($circle, fn($circle) => $circle->at(10, 10));

// draw circle object at new position
$image->drawCircle($circle, fn($circle) => $circle->at(100, 100));

// draw circle object at another position
$image->drawCircle($circle, fn($circle) => $circle->at(200, 200));
```

### Draw a Line

> public Image::drawLine(callable|Line $line, null|callable $adjustments = null): ImageInterface

Draw a line on the current image. Define the overall appearance of the
shape by passing an callback or a line object. Optionally you can pass an
adjustment callback to modify the given geometric object for this single call.

#### Parameters

| Name | Type | Description |
| - | - | - |
| line | callable or Intervention\Image\Geometry\line | The line or a callback on a line factory. See example. |
| adjustments | null or callable | A callable to adjust the appearance of the given line for this drawing operation. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\LineFactory;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// draw a line
$image->drawline(function (LineFactory $line): void {
    $line->from(10, 10);
    $line->to(180, 25);
    $line->color('ff5500'); // color of line
});
```

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\LineFactory;
use Intervention\Image\Geometry\Factories\Drawable;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// create color for the line
$color = Color::rgb(255, 55, 0);

// create line object to reuse in following calls
$line = Drawable::line(function (LineFactory $line) use ($color): void {
     $line->color($color->withTransparency(.7));
 });

// draw line object at position
$image->drawLine($line, fn($line) => $line->from(10, 10)->to(25, 25));

// draw line object at new position
$image->drawLine($line, fn($line) => $line->from(40, 40)->to(85, 85));

// draw line object at another position
$image->drawLine($line, fn($line) => $line->from(7, 0)->to(20, 10));
```

### Draw a Polygon

> public Image::drawPolygon(callable|Polygon $polygon, null|callable $adjustments = null): ImageInterface

Draw a polygon on the current image. Define the overall appearance of the
shape by passing an callback or a polygon object. Optionally you can pass an
adjustment callback to modify the given geometric object for this single call.

#### Parameters

| Name | Type | Description |
| - | - | - |
| polygon | callable or Intervention\Image\Geometry\Polygon | The polygon or a callback on a polygon factory. See example. |
| adjustments | null or callable | A callable to adjust the appearance of the given polygon for this drawing operation. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\PolygonFactory;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// draw a polygon
$image->drawpolygon(function (PolygonFactory $polygon): void {
    $polygon->background('ff5500'); // background color of polygon
    $polygon->point(100, 100);
    $polygon->point(10, 10);
    $polygon->point(20, 10);
    $polygon->point(90, 110);
    $polygon->point(130, 10);
});
```

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\PolygonFactory;
use Intervention\Image\Geometry\Factories\Drawable;

// create an test image from a file
$image = ImageManager::usingDriver(Driver::class)->read('test.png');

// create background colors for the polygon
$orange = Color::rgb(255, 55, 0);
$blue = Color::rgb(0, 0, 200, .2);

// create polygon object to reuse in following calls
$polygon = Drawable::polygon(function (PolygonFactory $polygon): void {
    $polygon->point(100, 100);
    $polygon->point(10, 10);
    $polygon->point(20, 10);
    $polygon->point(90, 110);
    $polygon->point(130, 10);
 });

// draw orange polygon object
$image->drawPolygon($polygon, fn($polygon) => $polygon->background($orange));

// draw blue polygon object
$image->drawPolygon($polygon, fn($polygon) => $polygon->background($blue));
```

### Draw Bezier Curves

> public Image::drawBezier(callable|Bezier $bezier, null|callable $adjustments = null): ImageInterface

This method draws [Bézier curves](https://en.wikipedia.org/wiki/B%C3%A9zier_curve), the 
shape of which is defined by a set of control points specified in the callback.
The type of curve drawn depends on the number of control points specified, 
which must be either three or four. With three control points, the result is a 
**quadratic Bézier curve**, while four points result in a **cubic Bézier curve**. The 
first and last control points define the start and end points of the curve.

The color, width and background color of the curve can also be set.

#### Parameters

| Name | Type | Description |
| - | - | - |
| init | Closure or Intervention\Image\Geometry\Bezier | Callback to define the appearance and position of the bézier curve or object. See example. |
| adjustments | null or callable | A callable to adjust the appearance of the given curve for this drawing operation. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;
use Intervention\Image\Geometry\Factories\BezierFactory;

// create a new image
$image = ImageManager::usingDriver(Driver::class)
    ->createImage(500, 500)
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
