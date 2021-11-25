# pickColor()
## Pick a color out of the current image

> public Intervention\Image\Image pickColor(int $x, int $y, [string $format])

Pick a color at **point x, y** out of current image and return in optional given **format**.

### Parameters

#### x
x-coordinate of the pixel the color is picked from.

#### y
y-coordinate of the pixel the color is picked from.

#### format (optional)
Select the color to be formated in one of the different types:

- **array**: `[255, 255, 255, 1]`
- **string (rgb)**: `rgb(255, 255, 255)`
- **string (rgba)**: `rgba(255, 255, 255, 0.5)`
- **string (hex)**: `#cccccc`
- **int**: `16776956`

By default the method returns the RGB value of that pixel as an array. Use the integer format to pass colors directly into any GD Library functions.

### Return Values
mixed - Depends on format parameter. By default an array of the RGB and alpha values.

### Examples

```php
// create an image
$img = Image::make('public/foo.jpg');

// pick a color at position as array
$arraycolor = $img->pickColor(100, 100);

// pick a color at position as integer
$intcolor = $img->pickColor(100, 100, 'int');

// pick a color at position and format it as hex string
$hexcolor = $img->pickColor(100, 100, 'hex');
```
