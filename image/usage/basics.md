# Basic Usage

- [Reading Images](#reading)
- [Creating Images](#creating)
- [Editing Images](#editing)
- [Saving Images](#saving)

---

<a name="reading"></a>
## Reading Images

Intervention Image makes it super easy to read images. The Library takes away any annoying work, the only thing you have to do is to give a file path to the method [make()](/api/make).

#### Read image from file

```php
$img = Image::make('foo/bar/baz.jpg');
```

The method is highly variable. It not only reads filepaths but also the following input formats.

- Path of the image in filesystem
- URL of an image
- Binary image data
- PHP resource of type gd
- Imagick instance
- Intervention\Image\Image instance

See more examples to initiate image instances in the [api documentation](/api/make).

---

<a name="creating"></a>
## Creating Images

If you want to create a new empty image instance you can call the [canvas()](/api/canvas) method with given width and height. Optionally it's possible to define a background-color, if not passed the default the canvas background is transparent.

#### Creating new images with background color

```php
$img = Image::canvas(800, 600, '#ccc');
```

See more examples to create new image instances in the [api documentation](/api/canvas).

---

<a name="editing"></a>
## Editing Images

After you initiated a new image instance with [make()](/api/make) or [canvas()](/api/canvas), you can use the whole palette of manipulation methods on the instance.

Usually each command returns a modified instance of Intervention\Image\Image, so you are able to chain methods.

#### Method chaining

```php
$img = Image::make('foo.jpg')->resize(320, 240)->insert('watermark.png');
```

Take a look at some of the methods in the following list.

### Resizing Images

- [resize()](/api/resize)
- [widen()](/api/widen)
- [heighten()](/api/heighten)
- [fit()](/api/fit)
- [resizeCanvas()](/api/resizeCanvas)
- [crop()](/api/crop)
- [trim()](/api/trim)

### Adjusting Images

- [gamma()](/api/gamma)
- [brightness()](/api/brightness)
- [contrast()](/api/contrast)
- [colorize()](/api/colorize)
- [greyscale()](/api/greyscale)
- [invert()](/api/invert)
- [mask()](/api/mask)
- [flip()](/api/flip)

### Applying Effects

- [filter()](/api/filter)
- [pixelate()](/api/pixelate)
- [rotate()](/api/rotate)
- [blur()](/api/blur)

### Drawing

- [text()](/api/text)
- [pixel()](/api/pixel)
- [line()](/api/line)
- [rectangle()](/api/rectangle)
- [circle()](/api/circle)
- [ellipse()](/api/ellipse)

### Retrieving Information

- [width()](/api/width)
- [height()](/api/height)
- [mime()](/api/mime)
- [exif()](/api/exif)


See the **api documentation** for the whole list of commands.

---

<a name="saving"></a>
## Saving Images

To save the current state of the image object in filesystem just call [save()](/api/save). Define optionally a certain path where the image should be saved. The image type will be defined by the file extension. For example if you pass foo.jpg the image will be saved as a JPG file. You can also optionally set the quality of the image file as second parameter.

#### Save an image in filesystem

```php
Image::make('foo.jpg')->resize(300, 200)->save('bar.jpg');
```

See more examples to save an image in the [api documentation](/api/save).
