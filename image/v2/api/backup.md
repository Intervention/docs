---
label: "backup()"
title: "Image::backup"
subtitle: "Save a backup of the current image state"
sort: 0
---

> public Intervention\Image\Image backup([string $name])

Backups current image state as fallback for [reset method](/v2/api/reset) under an optional **name**. Overwrites older state on every call, unless a different name is passed.

### Parameters

#### name (optional)
The name of the backup in memory. Default: *default*

### Return Values
Instance of `Intervention\Image\Image`

### Examples

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

### See also

- [reset](/v2/api/reset)
