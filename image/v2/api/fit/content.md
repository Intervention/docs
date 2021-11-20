> public Intervention\Image\Image fit(int $width, [[int $height], [Closure $callback, [string $position]]])

Combine cropping and resizing to format image in a smart way. The method will find the best fitting aspect ratio of your given **width and height** on the current image automatically, cut it out and resize it to the given dimension. You may pass an optional Closure **callback** as third parameter, to prevent possible upsizing and a custom **position** of the cutout as fourth parameter.


## Parameters

### width
The width the image will be resized to after cropping out the best fitting aspect ratio.

### height (optional)
The height the image will be resized to after cropping out the best fitting aspect ratio. If no height is given, method will use same value as width.

### callback (optional)
Closure callback defining constraint to prevent unwanted **upsizing** of the image. See examples below.

#### upsize

> public Intervention\Image\Size upsize()

Keep image from being upsized.

### position (optional)
Set a position where cutout will be positioned. By default the best fitting aspect ration is centered.

The possible values are:

- top-left
- top
- top-right
- left
- center (default)
- right
- bottom-left
- bottom
- bottom-right


## Return Values
Instance of `Intervention\Image\Image`

## Examples

```php
// open file a image resource
$img = Image::make('public/foo.jpg');

// crop the best fitting 5:3 (600x360) ratio and resize to 600x360 pixel
$img->fit(600, 360);

// crop the best fitting 1:1 ratio (200x200) and resize to 200x200 pixel
$img->fit(200);

// add callback functionality to retain maximal original image size
$img->fit(800, 600, function ($constraint) {
    $constraint->upsize();
});
```


## See also

- [resize](/api/resize)
- [resizeCanvas](/api/resizeCanvas)
- [crop](/api/crop)
- [trim](/api/trim)
