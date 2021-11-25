# text()
## Write text to the current image

> public Intervention\Image\Image text(string $text, [integer $x, [integer $y, [Closure $callback]]])

Write a **text** string to the current image at an optional **x,y basepoint position**. You can define more details like font-size, font-file and alignment via a **callback** as the fourth parameter.

### Parameters

#### text
The text string that will be written to the image.

#### x (optional)
x-ordinate defining the basepoint of the first character. Default: `0`

#### y (optional)
y-ordinate defining the basepoint of the first character. Default: `0`

#### callback (optional)
Closure callback on the font object to define more optional details. Use the following methods to pass details. See examples of the callback usage below.

> public Intervention\Image\Font file(string $filepath)

Set path to a True Type Font file or a integer value between 1 and 5 for one of the GD library internal fonts. Default: `1`

> public Intervention\Image\Font size(integer $size)

Set font size in pixels. **Font sizing is only available if a font file is set and will be ignored otherwise.** Default: `12`

> public Intervention\Image\Font color(mixed $color)

Set color of the text in one of the available [color formats](/getting_started/formats). Default: `#000000`

> public Intervention\Image\Font align(string $align)

Set horizontal text alignment relative to given basepoint. Possible values are left, right and center. Default: `left`

> public Intervention\Image\Font valign(string $valign)

Set vertical text alignment relative to given basepoint. Possible values are top, bottom and middle. Default: `bottom`

> public Intervention\Image\Font angle(integer $angle)

Set rotation angle of text in degrees. Text will be rotated counter-clockwise around the vertical and horizontal aligned point. **Rotation is only available if a font file is set and will be ignored otherwise**. Default: no rotation

### Return Values
Instance of `Intervention\Image\Image`

<a name="examples"></a>

### Examples

```php
// create Image from file
$img = Image::make('public/foo.jpg');

// write text
$img->text('The quick brown fox jumps over the lazy dog.');

// write text at position
$img->text('The quick brown fox jumps over the lazy dog.', 120, 100);

// use callback to define details
$img->text('foo', 0, 0, function($font) {
    $font->file('foo/bar.ttf');
    $font->size(24);
    $font->color('#fdf6e3');
    $font->align('center');
    $font->valign('top');
    $font->angle(45);
});

// draw transparent text
$img->text('foo', 0, 0, function($font) {
    $font->color([255, 255, 255, 0.5]);
});
```
