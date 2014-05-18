# widen — Resize image proportionally to given width

## Description

> public Intervention\Image\Image widen ( integer $width )

Resizes the current image to new **width**, constraining aspect ratio.

## Parameters

### width
The new width of the image

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// resize image new width
$img = Image::make('public/foo.jpg')->widen(300);
```


## See also

- [heighten](/api/heighten)
- [resize](/api/resize)
