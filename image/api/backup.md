# backup — backups current image state

## Description

> public Intervention\Image\Image backup()

Backups current image state as fallback for [reset method](/api/reset). Overwrites older states on every call.


## Parameters

none

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create empty canvas with black background
$img = Image::canvas(120, 90, '#000000');

// fill image with color
$img->fill('#b53717');

// backup image with colored background
$img->backup();

// fill image with tiled image
$img->fill('tile.png');

// return to colored background
$img->reset();
```

## See also

- [reset](/api/reset)
