# make — Create a new image resource

## Description

> public static Intervention\Image\Image make( mixed $source )

Universal factory method to create a new image instance from **source**, which can be a filepath, a GD image resource, an Imagick object or a binary image data.

## Parameters

### source

Source to create an image from. The method responds to the following input types:

- **string** - Path of the image in filesystem.
- **string** - URL of an image (```allow_url_fopen``` must be enabled).
- **string** - Binary image data.
- **string** - Data-URL encoded image data.
- **resource** - PHP resource of type gd.
- **object** - Imagick instance
- **object** - Intervention\Image\Image instance
- **object** - SplFileInfo instance

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create a new image resource from file
$img = Image::make('public/foo.jpg');

// create a new image resource from binary data
$data = file_get_contents('public/foo.jpg');
$img = Image::make($data);

// create a new image from gd resource
$resource = imagecreatefromjpeg('public/foo.jpg');
$img = Image::make($resource);

// create a new image directly from an url
$img = Image::make('http://example.com/example.jpg');

// create a new image directly from Laravel file upload
$img = Image::make(Input::file('photo'));
```

## See also

- [canvas](/api/canvas)
- [cache](/api/cache)

