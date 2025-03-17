# Image::limitColors
## Reduce number of colors for the current image

> public Intervention\Image\Image limitColors(integer $count, [mixed $matte])

Method converts the existing colors of the current image into a color table with a given maximum **count** of colors. The function preserves as much alpha channel information as possible and blends transarent pixels against a optional **matte color**.

### Parameters

#### count
Maximum number of colors that should be retained in the color palette. Or `null` to convert to truecolor.

#### matte (optional)
A color to blend transparent pixels against. Can be defined in one of the different [color formats](/v2/introduction/formats). Default: no matte color

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// open PNG-32 image from file
$img = Image::make('public/foo.png');

// limit colors to 255 (PNG-8) blending transparency against orange
$img->limitColors(255, '#ff9900');
```

### See also

- [save](/v2/api/save)
- [encode](/v2/api/encode)
