## Description

> public Intervention\Image\Image encode([mixed $format, [int $quality]])

Encodes the current image in given **format** and given **image quality**.

## Parameters

### format (optional)
Define the encoding format from one of the following formats:

- **jpg** — return JPEG encoded image data
- **png** — return Portable Network Graphics (PNG) encoded image data
- **gif** — return Graphics Interchange Format (GIF) encoded image data
- **tif** — return Tagged Image File Format (TIFF) encoded image data
- **bmp** — return Bitmap (BMP) encoded image data
- **ico** — return ICO encoded image data
- **psd** — return Photoshop Document (PSD) encoded image data
- **webp** — return WebP encoded image data
- **data-url** — encode current image data in data URI scheme (RFC 2397)

By default the method will return data encoded in the type of the current image. If no image type is defined yet, data will be encoded as jpeg.

### quality (optional)
Define the quality of the encoded image optionally. Data ranging from 0 (poor quality, small file) to 100 (best quality, big file). Quality is only applied if you're encoding JPG format since PNG compression is lossless and does not affect image quality. Default: 90.

## Return Values
Instance of Intervention\Image\Image with attached encoded image data. Instance can be casted to string to access data.

## Examples

```php
// encode png image as jpg
$jpg = (string) Image::make('public/foo.png')->encode('jpg', 75);

// encode image as data-url
$data = (string) Image::make('public/bar.png')->encode('data-url');
```


## See also

- [save](/api/save)
