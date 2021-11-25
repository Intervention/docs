# interlace()
## Enable or disabled interlaced mode of the current image

> public Intervention\Image\Image interlace([boolean $interlace])

Determine whether an image should be encoded in interlaced or standard mode by toggling **interlace** mode with a boolean parameter. If an JPEG image is set interlaced the image will be processed as a progressive JPEG.

### Parameters

#### interlace (optional)
If interlace is set to boolean `true` the image will be encoded interlaced. If the parameter is set to `false` interlaced mode is turned off. Default: `true`


### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// open image
$img = Image::make('public/foo.png');

// enable interlacing
$img->interlace();

// save image interlaced
$img->save();

// open interlaced image
$img = Image::make('public/interlaced.gif');

// disable interlacing
$img->interlace(false);

// save image in standard mode
$img->save();
```

### See also

- [limitColors](/v2/api/limitColors)
- [save](/v2/api/save)
- [encode](/v2/api/encode)
