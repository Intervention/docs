---
label: "height()"
title: "Image::height"
subtitle: "Get the height in pixels of the current image"
sort: 22
---

> public Intervention\Image\Image height()

Returns the height in pixels of the current image.

### Parameters

none

### Return Values
Height of current image as integer

### Examples

```php
// read height of image
$height = Image::make('public/foo.jpg')->height();
```

## See also

- [width](/v2/api/width)
