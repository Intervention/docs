## Description

> public Intervention\Image\Image filesize()

Gets the file size for the current image, if instance is initiated from an actual file.

## Parameters

none


## Return Values

Returns the size of the image file in bytes or `false` if image instance is not created from a file.

Examples

```php
// create an image
$img = Image::make('public/foo.jpg');

// get file size
$size = $img->filesize();
```
