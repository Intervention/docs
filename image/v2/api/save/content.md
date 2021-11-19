## Description

> public Intervention\Image\Image save([string $path, [int $quality], [string $format]])

Save the current state of the image object in filesystem. Define optionally a certain **path** where the image should be saved. You can also optionally set the **quality** of the image file as second parameter.

The image type will be defined by the file extension. For example if you pass ```foo.jpg``` the image will be saved as a JPG file. If there is no extension available, the library will first try to use the MIME type of the image to define the encoding, if this also fails the image will be encoded as JPEG. Optionally you can override this with the format parameter.

Furthermore the image will always be saved in RGB color mode without an embeded color profile.

## Parameters

### path (optional)
Path to the file where to write the image data. If the image is created from a existing image in the filesystem and the parameter is not set, the method will try to overwrite the existing file.

### quality (optional)
Define optionally the quality of the image. It is normalized for all file types to a range from 0 (poor quality, small file) to 100 (best quality, big file). Quality is only applied if you're encoding JPG format since PNG compression is lossless and does not affect image quality. The default value is 90.

### format (optional)
By default the format of the saved image is defined by the file extension of the given path. Alternatively it is possible to define the image format by passing one of the [image format extension](/getting_started/formats) as a third parameter.


## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// open and resize an image file
$img = Image::make('public/foo.jpg')->resize(300, 200);

// save file as jpg with medium quality
$img->save('public/bar.jpg', 60);

// save the same file as jpg with default quality
$img->save('public/baz.jpg');

// save the file in png format
$img->save('public/bar.png');

// save the image jpg format defined by third parameter
$img->save('public/foo', 80, 'jpg');
```

See also

- [make](/api/make)
- [encode](/api/encode)
