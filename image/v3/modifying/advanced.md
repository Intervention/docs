# Advanced
## Advanced Image Modification
Discover the endless possibilities of Intervention Image by directly accessing the native image data and combining them with custom modifier classes.

If the supplied options are not sufficient, it is possible to create your own
solutions using your own [custom modifiers](/v3/modifying/custom-modifiers).
Furthermore, the native image object can be accessed, so that all functions
used by the actual image processing libraries (such as GD or Imagick) can be used
- even those not covered by Intervention Image.

## Access the Native Image Object

Depending on the driver, each image object is mapped internally by either an
instance of a `GDImage::class` or an `Imagick::class` object. The parent image object of
Intervention Image provides access to this base object.

The following example uses the native Imagick function
[oilPaintImage()](https://www.php.net/manual/en/imagick.oilpaintimage.php),
which is not included in this library.

```php
use Intervention\Image\ImageManager;

// read test image from a file
$manager = ImageManager::imagick();
$image = $manager->read('test.png');

// access Imagick instance directly
$imagick = $image->core()->native();

// use external Imagick function
$imagick->oilPaintImage(4.5);
```

Combined with [custom modifiers](/v3/modifying/custom-modifiers), Intervention
Image can be extended with your own modifier combinations for endless
possibilities.
