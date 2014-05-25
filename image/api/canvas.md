# canvas — Create a new empty image resource

## Description

> public Intervention\Image\Image canvas(integer $width, integer $height, [mixed $bgcolor])

Factory method to create a new empty image instance with given **width and height**. You can define a **background-color** optionally. By default the canvas background is transparent.

## Parameters

### width
Width of the new image resource.

### height
Height of the new image resource.

### bgcolor (optional)
Optional Background-color of the image resource. Pass a color in one of the supported [color formats](/getting_started/formats) or just leave it blank to get a transparent background.


## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// create a new empty image resource with transparent background
$img = Image::canvas(800, 600);

// create a new empty image resource with red background
$img = Image::canvas(32, 32, '#ff0000');
```


## See also

- [make](/api/make)
- [cache](/api/cache)