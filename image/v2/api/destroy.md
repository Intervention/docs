# Image::destroy
## Free up memory

> public Intervention\Image\Image destroy()

Frees memory associated with the current image instance **before** the PHP script ends. Normally resources are destroyed automatically **after** the script is finished.

Of course, the image instance is no longer usable after the method has been called.

### Parameters
none

### Return Values
none

### Examples

```php
// create an image
$img = Image::make('public/foo.jpg');

// perform some modifications
$img->resize(320, 240);
$img->save('public/small.jpg');

// destroy resource
$img->destroy();
```
