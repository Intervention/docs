# invert — Invert colors of an image

## Description

> public Intervention\Image\Image invert()

Reverses all colors of the current image.


## Parameters

none


## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create Image from file and reverse colors
$img = Image::make('public/foo.jpg')->invert();
```

## See also

- [brightness](/api/brightness)
- [contrast](/api/contrast)

