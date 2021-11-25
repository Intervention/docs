# opacity()
## Set opacity of the current image

> public Intervention\Image\Image opacity(integer $transparency)

Set the **opacity** in percent of the current image ranging from 100% for opaque and 0% for full transparency.

**Note: Performance intensive on larger images. Use with care.**

### Parameters

#### transparency
The new percent of transparency as integer for the current image.

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create Image from file and set transparency to 50%
Image::make('public/foo.jpg')->opacity(50);

// create new Intervention Image from file and set image full transparent
$img = Image::make('public/foo.jpg');
$img->opacity(0);
```

### See also

- [fill](/v2/api/fill)
- [mask](/v2/api/mask)
