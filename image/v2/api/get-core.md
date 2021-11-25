# getCore()
## Read core instance of the current image

> public Intervention\Image\Image getCore()

Returns the current image in core format of the particular driver. If you're using GD, you will get the the current **GD resource** as return value. If you have setup the Imagick driver, the method will return the current image information as an **Imagick object**.

### Parameters

none

### Return Values

mixed - depends on configured driver

### Examples

```php
// create Intervention Image
$img = Image::make('public/foo.jpg');

// get Imagick instance
$imagick = $img->getCore();

// apply Imagick function
$imagick->embossImage(0, 1);
```
