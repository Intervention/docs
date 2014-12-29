# iptc — Reads IPTC meta data from image

## Description

> public Intervention\Image\Image iptc([string $key])

Read IPTC meta data from current image.

## Parameters

### key (optional)
Optionally index key to retrieve only particular value. By default all data available will be parsed.


## Return Values
Associative array of all meta data values available or mixed data for particular value. If no meta data can be found, method will return NULL.


## Examples

```php
// read all existing data into an array
$data = Image::make('public/foo.jpg')->iptc();

// read only 'Copyright'
$copyright = Image::make('public/foo.jpg')->iptc('Copyright');
```

## See also

- [exif](/api/exif)
- [orientate](/api/orientate)
