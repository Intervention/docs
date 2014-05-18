# heighten — Resize image proportionally to given height

## Description

> public Intervention\Image\Image heighten ( integer $height )

Resizes the current image to new **height**, constraining aspect ratio.

## Parameters

### height
The new height of the image

## Return Values
Resized instance of Intervention\Image\Image

## Examples

```php
// resize image new height
$img = Image::make('public/foo.jpg')->heighten(100);
```

## See also

- [widen](/api/widen)
- [resize](/api/resize)
