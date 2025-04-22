---
label: "width()"
title: "Image::width"
subtitle: "Get width of current image"
---

> public Intervention\Image\Image width()

Returns the width in pixels of the current image.

### Parameters

none

### Return Values
Width of current image in pixels as integer

### Examples

```php
// read width of image
$width = Image::make('public/foo.jpg')->width();
```

### See also

- [height](/v2/api/height)
