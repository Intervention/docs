# response — Attach image to new HTTP response

## Description

> public Intervention\Image\Image response([string $format, [integer $quality]])

Sends HTTP response with current image in given **format** and **quality**.

## Parameters

### format (optional)
Define the encoding format from one of the following formats:

- **jpg** — return JPEG encoded image data
- **png** — return Portable Network Graphics (PNG) encoded image data
- **gif** — return Graphics Interchange Format (GIF) encoded image data
- **tif** — return Tagged Image File Format (TIFF) encoded image data
- **bmp** — return Bitmap (BMP) encoded image data

By default the response data will be encoded in the type of the current image. If no image type is defined yet, method will return jpeg encoded data.

### quality (optional)
Define optionally the quality encoded image data ranging from 0 (poor quality, small file) to 100 (best quality, big file). Default: ```90```.


## Return Values
Encoded image data after raw HTTP header is sent. If you are in a **Laravel framework** environment the method will return a **Illuminate\Http\Response** with the corresponding header fields already set.

## Examples

#### Basic Example

```php
// create a new empty image resource
$img = Image::canvas(800, 600, '#ff0000');

// send HTTP header and output image data
echo $img->response();
```

#### Laravel Example

```php
Route::get('/', function()
{
    return Image::make('foo/bar.jpg')->response('png');
});
```

## See also

- [encode](/api/encode)
- [save](/api/save)
- [cache](/api/cache)
