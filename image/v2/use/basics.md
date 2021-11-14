# Basic Usage

- [Reading Images](#reading)
- [Creating Images](#creating)
- [Editing Images](#editing)
- [Outputting Images](#output)

---

<a name="reading"></a>
## Quickstart

#### Example

```php
// include composer autoload
require 'vendor/autoload.php';

// import the Intervention Image Manager Class
use Intervention\Image\ImageManager;

// create an image manager instance with favored driver
$manager = new ImageManager(array('driver' => 'imagick'));

// to finally create image instances
$image = $manager->make('public/foo.jpg')->resize(300, 200);
```

You might also use the static version of ImageManager as shown in the example below.

#### Static Example

```php
// include composer autoload
require 'vendor/autoload.php';

// import the Intervention Image Manager Class
use Intervention\Image\ImageManagerStatic as Image;

// configure with favored image driver (gd by default)
Image::configure(array('driver' => 'imagick'));

// and you are ready to go ...
$image = Image::make('public/foo.jpg')->resize(300, 200);
```

You can read more detailed information about [installation](/getting_started/installation) and [configuration](/getting_started/configuration).

---



<a name="reading"></a>
## Reading Images

Intervention Image makes it super easy to read images. The Library takes away any annoying work, the only thing you have to do is to give a file path to the method [make()](/api/make).

#### Read image from file

```php
$img = Image::make('foo/bar/baz.jpg');
```

The method is highly variable. It not only reads filepaths but also the following input formats.

- Path of the image in filesystem.
- URL of an image (```allow_url_fopen``` must be enabled).
- Binary image data.
- Data-URL encoded image data.
- Base64 encoded image data.
- PHP resource of type gd. (when using GD driver)
- Imagick instance (when using Imagick driver)
- Intervention\Image\Image instance
- SplFileInfo instance (To handle Laravel file uploads via Symfony\Component\HttpFoundation\File\UploadedFile)

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
- [iptc()](/api/iptc)


See the **api documentation** for the whole list of commands.

---

<a name="output"></a>
## Outputting Images

To create actually image data from an image object, you can access methods like [encode](/api/encode) to create encoded image data or use [save](/api/save) to write an image into the filesystem. It's also possible to send a HTTP [response](/api/response) with current image data.

#### Save an image in filesystem

```php
Image::make('foo.jpg')->resize(300, 200)->save('bar.jpg');
```

Read more about [image HTTP responses](/use/http).

### Outputting Image data

- [encode()](/api/encode)
- [save()](/api/save)
- [response()](/api/response)
