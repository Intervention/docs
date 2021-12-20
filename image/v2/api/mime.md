# Image::mime
## Get MIME Type of the current image

> public Intervention\Image\Image mime()

Read MIME Type of current image instance, if it's already defined.

### Parameters

none

### Return Values
MIME Type of current image.

### Examples

```php
// read mime type of image
$mime = Image::make('public/foo.jpg')->mime();
```

### See also

- [width](/v2/api/width)
- [height](/v2/api/height)
- [exif](/v2/api/exif)
