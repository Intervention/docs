---
label: "resize()"
title: "Image::resize"
subtitle: "Resize the current image"
---

> public Intervention\Image\Image resize (integer $width, integer $height, Closure $callback)

Resizes current image based on given **width** and/or **height**. To constraint the resize command, pass an optional Closure **callback** as third parameter.
    
### Parameters

#### width
The new width of the image

#### height
The new height of the image

#### callback (optional)

Closure callback defining constraints on the resize. It's possible to constraint the **aspect-ratio** and/or a unwanted **upsizing** of the image. See examples below.

> public Intervention\Image\Size aspectRatio()

Constraint the current aspect-ratio of the image. As a shortcut to proportional resizing you can use [widen()](/v2/api/widen) or [heighten()](/v2/api/heighten).

> public Intervention\Image\Size upsize()

Keep image from being upsized.

### Return Values
Instance of `Intervention\Image\Image`

### Examples

```php
// create instance
$img = Image::make('public/foo.jpg');

// resize image to fixed size
$img->resize(300, 200);

// resize only the width of the image
$img->resize(300, null);

// resize only the height of the image
$img->resize(null, 200);

// resize the image to a width of 300 and constrain aspect ratio (auto height)
$img->resize(300, null, function ($constraint) {
    $constraint->aspectRatio();
});

// resize the image to a height of 200 and constrain aspect ratio (auto width)
$img->resize(null, 200, function ($constraint) {
    $constraint->aspectRatio();
});

// prevent possible upsizing
$img->resize(null, 400, function ($constraint) {
    $constraint->aspectRatio();
    $constraint->upsize();
});

// resize the image so that the largest side fits within the limit; the smaller
// side will be scaled to maintain the original aspect ratio
$img->resize(400, 400, function ($constraint) {
    $constraint->aspectRatio();
    $constraint->upsize();
});
```

### See also

- [widen](/v2/api/widen)
- [heighten](/v2/api/heighten)
- [fit](/v2/api/fit)
- [resizeCanvas](/v2/api/resize-canvas)
- [crop](/v2/api/crop)
- [trim](/v2/api/trim)
