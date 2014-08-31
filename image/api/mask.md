# mask — Apply an alpha mask to an image

## Description

> public Intervention\Image\Image mask( mixed $source, [bool $mask_with_alpha] )

Apply a given **image source** as alpha mask to the current image to change current opacity. Mask will be resized to the current image size. By default a greyscale version of the mask is converted to alpha values, but you can set **mask_with_alpha** to apply the actual alpha channel. Any transparency values of the current image will be maintained. 


## Parameters

### source
The image source that will be applied as alpha mask. The method can handle the following types of input:

- **string** - Path of the image in filesystem.
- **string** - URL of an image (```allow_url_fopen``` must be enabled).
- **string** - Binary image data.
- **string** - Data-URL encoded image data.
- **resource** - PHP resource of type gd.
- **object** - Imagick instance
- **object** - Intervention\Image\Image instance
- **object** - Symfony\Component\HttpFoundation\File\UploadedFile instance


### mask_with_alpha (optional)
Set this to ```true``` to apply the actual alpha channel as mask to the current image instead of the color values. Default: false

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create new Intervention Image
$img = Image::make('public/foo.jpg');

// Apply another image as alpha mask on image
$img->mask('public/mask.png');

// Apply a second image with alpha channel masking
$img->mask('public/alpha.png', true);
```

## See also

- [fill](/api/fill)
- [opacity](/api/opacity)
- [insert](/api/insert)
