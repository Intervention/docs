# flip()
## Mirror the current image vertically or horizontally

> public Intervention\Image\Image flip([string $mode])

Mirror the current image horizontally or vertically by specifying the **mode**.

### Parameters

#### mode (optional)
Specify the mode the image will be flipped. You can set ```h``` for horizontal (default) or ```v``` for vertical flip.

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create Image from file
$img = Image::make('public/foo.jpg');

// flip image vertically
$img->flip('v');
```

### See also

- [rotate](/v2/api/rotate)