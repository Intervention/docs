# Image::rotate
## Rotate the current image

> public Intervention\Image\Image rotate(float $angle, [string $bgcolor])

Rotate the current image counter-clockwise by a given **angle**. Optionally define a **background color** for the uncovered zone after the rotation.

### Parameters

#### angle
The rotation angle in degrees to rotate the image counter-clockwise.

#### bgcolor (optional)
A background color for the uncovered zone after the rotation. The background color can be passed in different [color formats](/getting_started/formats). Default: `#ffffff`, transparent if supported by the output format


### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create Image from file
$img = Image::make('public/foo.jpg');

// rotate image 45 degrees clockwise
$img->rotate(-45);
```

### See also

- [flip](/v2/api/flip)
- [resize](/v2/api/resize)
- [resizeCanvas](/v2/api/resizeCanvas)
