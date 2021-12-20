# Image::psrResponse
## Attach the current image to new PSR-7 HTTP response

> public Intervention\Image\Image psrResponse([mixed $format, [int $quality]])

Encodes the current image in given **format** and given **image quality** and creates new PSR-7 HTTP response based on image data.

### Parameters

#### format (optional)
Define the encoding format from one of the following formats:

- **jpg** — return JPEG encoded image data
- **png** — return Portable Network Graphics (PNG) encoded image data
- **gif** — return Graphics Interchange Format (GIF) encoded image data
- **tif** — return Tagged Image File Format (TIFF) encoded image data
- **bmp** — return Bitmap (BMP) encoded image data
- **data-url** — encode current image data in data URI scheme (RFC 2397)

By default the method will return data encoded in the type of the current image. If no image type is defined yet, data will be encoded as jpeg.

#### quality (optional)
Define the quality of the encoded image optionally. Data ranging from `0` (poor quality, small file) to `100` (best quality, big file). Quality is only applied if you're encoding JPG format since PNG compression is lossless and does not affect image quality. Default: `90`.

### Return Values
[PSR-7 HTTP response](http://www.php-fig.org/psr/psr-7/) as instance of `GuzzleHttp\Psr7\Response`.

### Examples

```php
// encode png image as jpg stream
$response = Image::make('public/foo.png')->psrResponse('jpg', 60);
```

### See also

- [stream](/v2/api/stream)
- [encode](/v2/api/encode)
- [save](/v2/api/save)
