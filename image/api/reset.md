# reset — Reset image instance

## Description

> public Intervention\Image\Image reset()

Resets all of the modifications to a state saved previously by [backup](/api/backup).

## Parameters

none


## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create an image
$img = Image::make('public/foo.jpg');

// backup status
$img->backup();

// perform some modifications
$img->resize(320, 240);
$img->invert();
$img->save('public/small.jpg');

// reset image (return to backuped state)
$img->reset();

// perform other modifications
$img->resize(640, 480);
$img->invert();
$img->save('public/large.jpg');
```

## See also

- [backup](/api/backup)
