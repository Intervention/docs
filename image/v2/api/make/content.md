## Description

> public static Intervention\Image\ImageManager make(mixed $source)

Universal factory method to create a new image instance from **source**. The method is highly variable to read all the input types listed below.

## Parameters

### source

Source to create an image from. The method responds to the following input types:

- **string** - Path of the image in filesystem.
- **string** - URL of an image (```allow_url_fopen``` must be enabled).
- **string** - Binary image data.
- **string** - Data-URL encoded image data.
- **string** - Base64 encoded image data.
- **resource** - PHP resource of type gd. (when using GD driver)
- **object** - Imagick instance (when using Imagick driver)
- **object** - Intervention\Image\Image instance
- **object** - SplFileInfo instance (To handle Laravel file uploads via Symfony\Component\HttpFoundation\File\UploadedFile)

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create a new image resource from file
$img = Image::make('public/foo.jpg');

// or create a new image resource from binary data
$img = Image::make(file_get_contents('public/foo.jpg'));

// create a new image from gd resource
$img = Image::make(imagecreatefromjpeg('public/foo.jpg'));

// create a new image directly from an url
$img = Image::make('http://example.com/example.jpg');

// create a new image directly from Laravel file upload
$img = Image::make(Input::file('photo'));
```

## See also

- [canvas](/api/canvas)
- [cache](/api/cache)

