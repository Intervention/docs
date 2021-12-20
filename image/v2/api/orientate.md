# Image::orientate
## Adjusts the current image orientation automatically

> public Intervention\Image\Image orientate()

This method reads the EXIF image profile setting 'Orientation' and performs a rotation on the image to display the image correctly. **Image object must be instantiated from file path to read the EXIF data correctly.**

**Note: PHP must be compiled in with `--enable-exif` to use this method. Windows users must also have the `mbstring` extension enabled.**

### Parameters

None

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// instantiate image with auto-orientation
$img = Image::make('foo.jpg')->orientate();
```

### See also

- [exif](/v2/api/exif)
