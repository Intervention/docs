# mime — Get MIME Type

## Description

> public Intervention\Image\Image mime()

Read MIME Type of current image instance, if it's already defined.

## Parameters

none

## Return Values
MIME Type of current image.

Examples

```php
// read mime type of image
$mime = Image::make('public/foo.jpg')->mime();
```

## See also

- [width](/api/width)
- [height](/api/height)
- [exif](/api/exif)
