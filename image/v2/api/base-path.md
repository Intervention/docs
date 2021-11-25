# basePath()
## Get fully qualified path

> public Intervention\Image\Image basePath()

Get the base path for the current image, if instance was initiated from an actual file.

### Parameters

none

### Return Values

Returns the absolute path of the image file as `string` or `null` if the image instance wasn't created from a file.

Examples

```php
// create an image
$img = Image::make('public/foo.jpg');

// get file path
$path = $img->basePath();
```
