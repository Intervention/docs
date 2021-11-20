> public Intervention\Image\Image widen(integer $width, [Closure $callback])

Resizes the current image to new **width**, constraining aspect ratio. Pass an optional Closure **callback** as third parameter, to apply additional constraints like preventing possible upsizing.

## Parameters

### width
The new width of the image

### callback (optional)
Closure callback defining constraint to prevent unwanted **upsizing** of the image. See examples below.

#### upsize

> public Intervention\Image\Size upsize()

Keep image from being upsized.

## Return Values
Instance of `Intervention\Image\Image`

## Examples

```php
// resize image to new width
$img = Image::make('public/foo.jpg')->widen(300);

// resize image to new width but do not exceed original size
$img = Image::make('public/foo.jpg')->widen(300, function ($constraint) {
    $constraint->upsize();
});
```

## See also

- [heighten](/api/heighten)
- [resize](/api/resize)
