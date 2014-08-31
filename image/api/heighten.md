# heighten — Resize image proportionally to given height

## Description

> public Intervention\Image\Image heighten ( integer $height, [Closure $callback] )

Resizes the current image to new **height**, constraining aspect ratio. Pass an optional Closure **callback** as third parameter, to apply additional constraints like preventing possible upsizing.

## Parameters

### height
The new height of the image

### callback (optional)
Closure callback defining constraint to prevent unwanted **upsizing** of the image. See examples below.

#### upsize

> public Intervention\Image\Size upsize()

Keep image from being upsized.



## Return Values
Resized instance of Intervention\Image\Image

## Examples

```php
// resize image to new height
$img = Image::make('public/foo.jpg')->heighten(100);

// resize image to new height but do not exceed original size
$img = Image::make('public/foo.jpg')->heighten(100, function ($constraint) {
    $constraint->upsize();
});
```

## See also

- [widen](/api/widen)
- [resize](/api/resize)
