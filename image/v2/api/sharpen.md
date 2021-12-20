# Image::sharpen
## Sharpen the current image

> public Intervention\Image\Image sharpen([integer $amount])

Sharpen current image with an optional **amount**. Use values between `0` and `100`.

### Parameters

#### amount (optional)
The amount of the sharpening strength. Method accepts values between `0` and `100`. Default: `10`

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// sharpen image
$img->sharpen(15);
```

### See also

- [blur](/v2/api/blur)
