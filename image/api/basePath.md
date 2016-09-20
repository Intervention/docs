# basePath — Get fully qualified path

## Description

> public Intervention\Image\Image basePath()

Gets the file size for the current image, if instance is initiated from an actual file.

## Parameters

none


## Return Values

Returns the absolute path of the image file as `string` or `null` if the image instance isn't created from a file.

Examples

```php
// create an image
$img = Image::make('public/foo.jpg');

// get file path
$path = $img->basePath();
```
