# trim — Trim away parts of an image

## Description

> public Intervention\Image\Image trim( [string $base, [array $away, [int $tolerance, [int $feather]]]] )

Trim away image space in given color. Define an optional **base** to pick a color at a certain position and borders that should be trimmed **away**. You can also set an optional **tolerance** level, to trim similar colors and add a **feathering** border around the trimed image.

<div class="note">Note: Resource intensive with GD driver. Use with care.</div>

## Parameters

### base
Define the the point from where the trimming color is picked. For example if you set this parameter to ```bottom-right```, all color will be trimmed away that is equal to the color in the bottom-left corner of the image.

Possible values are:

- top-left (default)
- bottom-right
- transparent

### away (optional)
Border(s) that should be trimmed away. You can add multiple borders. as an array of values. Possible values are:

- top
- bottom
- left
- right

By default the trimming is performed on all borders.

### tolerance (optional)
Define a percentaged tolerance level between 0 and 100 to trim away similar color values. Default: 0

### feather (optional)
Sometimes it may be useful to leave a untouched "border" around an object while trimming. Especially when trimming non-solid backgrounds you can expand (positive value) or contract (negative value) the space around the trimed object by a certain amount of pixels. Default: 0


## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// trim image (by default on all borders with top-left color)
Image::make('public/foo.jpg')->trim();

// trim image (on all borders with bottom-right color)
Image::make('public/foo.jpg')->trim('bottom-right');

// trim image (only top and bottom with transparency)
Image::make('public/foo.jpg')->trim('transparent', array('top', 'bottom'));

// trim image (only left side top-left color)
Image::make('public/foo.jpg')->trim('top-left', 'left');

// trim image on all borders (with 40% tolerance)
Image::make('public/foo.jpg')->trim('top-left', null, 40);

// trim image and leave a border of 50px by feathering
Image::make('public/foo.jpg')->trim('top-left', null, 25, 50);
```

## See also

- [resize](/api/resize)
- [resizeCanvas](/api/resizeCanvas)
- [fit](/api/fit)
- [crop](/api/crop)
