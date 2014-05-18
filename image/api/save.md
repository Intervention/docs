# save — Save image in filesystem

## Description

> public Intervention\Image\Image save( [string $path, [int $quality]] )

Save the current state of the image object in filesystem. Define optionally a certain **path** where the image should be saved. The image type will be defined by the file extension. For example if you pass ```foo.jpg``` the image will be saved as a JPG file. You can also optionally set the **quality** of the image file as second parameter.


## Parameters

### path (optional)
Path to the file where to write the image data. If the image is created from a existing image in the filesystem and the parameter is not set, the method will try to overwrite the existing file.

### quality (optional)
Define optionally the quality of the image. It is normalized for all file types to a range from 0 (poor quality, small file) to 100 (best quality, big file). Quality is only applied if you're encoding JPG format since PNG compression is lossless and does not affect image quality. The default value is 90.


## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// open and resize an image file
$img = Image::make('public/foo.jpg')->resize(300, 200);

// save file as png with medium quality
$img->save('public/bar.png', 60);

// save the same file as jpeg with default quality
$img->save('public/bar.jpg');
```

See also

[make](/api/make)
[open](/api/open)
