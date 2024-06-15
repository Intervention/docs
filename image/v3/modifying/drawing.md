# Drawing
## Draw Colors & Shapes on Images

[TOC]

## Colors

### Fill Images with Color

> public Image::fill(mixed $color, ?int $x = null, ?int $y = null): ImageInterface

Fills the current image with the passed color specification. Optionally it is
possible to pass a position where the color fill should start. If these X and Y
values are set the color will be applied with Flood Fill. This means that only
colors that are at the specified position will be filled. If no position is
passed, the whole image will be filled.

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | mixed | Fill color in one of the different [color formats](/v3/introduction/formats#color-formats) |
| x | int | Optional x-coordinate of the filling position |
| y | int | Optional y-coordinate of the filling position |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(Driver::class);

// reading an image
$image = $manager->read('images/example.png');

// flood fill image with color
$image = $image->fill('#b53717', 10, 10);
```

## Geometric Shapes

### Draw a Pixel

> public Image::drawPixel(int $x, int $y, mixed $color = null): ImageInterface

Draw a single pixel at given position defined by the coordinates **x** and **y** in a given **color**.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | integer | Position of pixel on x-axis of the current image |
| y | integer | Position of pixel on y-axis of the current image |
| color | mixed | Color of the pixel in a [valid format](/v3/introduction/formats#color-formats) |


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

### Draw a Rectangle

> public Image::drawRectangle(int $x, int $y, ?callable $init = null): ImageInterface

Draw a colored rectangle on the current image with its top left position at the **x, y** coordinates. Define the overall appearance of the shape by passing a **init** callback as an optional parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | integer | Position of the top left corner of the rectangle on x-axis of the current image |
| y | integer | Position of the top left corner of the rectangle on y-axis of the current image |
| init | callable | Callback to define the appearance of the rectangle. See example. |

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

> public Image::drawEllipse(int $x, int $y, ?callable $init = null): ImageInterface

Draw a colored ellipse on the current image with its center position at the **x, y** coordinates. Define the overall appearance of the shape by passing a **init** callback as an optional parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | integer | Position of the center of the ellipse on x-axis of the current image |
| y | integer | Position of the center of the ellipse on y-axis of the current image |
| init | callable | Callback to define the appearance of the ellipse. See example. |

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

> public Image::drawCircle(int $x, int $y, ?callable $init = null): ImageInterface

Draw a colored circle on the current image with its center position at the **x, y** coordinates. Define the overall appearance of the shape by passing a **init** callback as an optional parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| x | integer | Position of the center of the circle on x-axis of the current image |
| y | integer | Position of the center of the circle on y-axis of the current image |
| init | callable | Callback to define the appearance of the circle. See example. |

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

> public Image::drawLine(?callable $init = null): ImageInterface

Draw a line on the current image. Define the overall appearance of the shape by passing a **init** callback as an optional parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| init | callable | Callback to define the appearance of the line. See example. |

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

> public Image::drawPolygon(callable $init): ImageInterface

Draw a polygon on the current image. Define the overall appearance of the shape by passing a **init** callback as an optional parameter.

#### Parameters

| Name | Type | Description |
| - | - | - |
| init | callable | Callback to define the appearance of the line. See example. |

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

### Universal Draw Method

> public Image::draw(DrawableInteface $drawable): ImageInterface

This universal method takes all objects that implement DrawableInterface::class and draws them on the current image instance.

This can be useful if you want to draw a shape repeatedly in different sizes, but do not want to call the callback again and again.

#### Parameters

| Name | Type | Description |
| - | - | - |
| drawable | DrawableInteface | Geometric shape to be drawn on the image. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Geometry\Factories\Drawable;

// create an test image from a file
$manager = ImageManager::imagick();
$image = $manager->read('test.png');

// create circle
$circle = Drawable::circle()
    ->border('ff0055')
    ->position(200, 200)
    ->create();

$rectangle = Drawable::rectangle()
    ->border('ff0055')
    ->position(100, 100)
    ->size(200, 200)
    ->create();

// draw circle instance with 100px diameter
$image->draw($circle->setDiameter(100));

// draw same circle instance with different diameter
$image->draw($circle->setDiameter(150));

// draw rectangle
$image->draw($rectangle);
```
