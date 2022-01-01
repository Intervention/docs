# Usage Overview
## Overview of the main use cases

[TOC]

## Basic Usage

#### Example

```php
// include composer autoload
require 'vendor/autoload.php';

// import the Intervention Image Manager Class
use Intervention\Image\ImageManager;

// create an image manager instance with favored driver
$manager = new ImageManager(['driver' => 'imagick']);

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
Image::configure(['driver' => 'imagick']);

// and you are ready to go ...
$image = Image::make('public/foo.jpg')->resize(300, 200);
```

You can read more detailed information about [installation](/v2/introduction/installation) and [configuration](/v2/introduction/configuration).

## Reading Images

Intervention Image makes it super easy to read images. The Library takes away any annoying work, the only thing you have to do is to give a file path to the method [make()](/v2/api/make).

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

See more examples to initiate image instances in the [api documentation](/v2/api/make).

## Creating Images

If you want to create a new empty image instance you can call the [canvas()](/v2/api/canvas) method with given width and height. Optionally it's possible to define a background-color, if not passed the default the canvas background is transparent.

#### Creating new images with background color

```php
$img = Image::canvas(800, 600, '#ccc');
```

See more examples to create new image instances in the [api documentation](/v2/api/canvas).

## Editing Images

After you initiated a new image instance with [make()](/v2/api/make) or [canvas()](/v2/api/canvas), you can use the whole palette of manipulation methods on the instance.

Usually each command returns a modified instance of Intervention\Image\Image, so you are able to chain methods.

#### Method chaining

```php
$img = Image::make('foo.jpg')->resize(320, 240)->insert('watermark.png');
```

Take a look at some of the methods in the following list.

### Resizing Images

- [resize()](/v2/api/resize)
- [widen()](/v2/api/widen)
- [heighten()](/v2/api/heighten)
- [fit()](/v2/api/fit)
- [resizeCanvas()](/v2/api/resize-canvas)
- [crop()](/v2/api/crop)
- [trim()](/v2/api/trim)

### Adjusting Images

- [gamma()](/v2/api/gamma)
- [brightness()](/v2/api/brightness)
- [contrast()](/v2/api/contrast)
- [colorize()](/v2/api/colorize)
- [greyscale()](/v2/api/greyscale)
- [invert()](/v2/api/invert)
- [mask()](/v2/api/mask)
- [flip()](/v2/api/flip)

### Applying Effects

- [filter()](/v2/api/filter)
- [pixelate()](/v2/api/pixelate)
- [rotate()](/v2/api/rotate)
- [blur()](/v2/api/blur)

### Drawing

- [text()](/v2/api/text)
- [pixel()](/v2/api/pixel)
- [line()](/v2/api/line)
- [rectangle()](/v2/api/rectangle)
- [circle()](/v2/api/circle)
- [ellipse()](/v2/api/ellipse)

### Retrieving Information

- [width()](/v2/api/width)
- [height()](/v2/api/height)
- [mime()](/v2/api/mime)
- [exif()](/v2/api/exif)
- [iptc()](/v2/api/iptc)


See the **api documentation** for the whole list of commands.

## Image Output

To create actually image data from an image object, you can access methods like [encode](/v2/api/encode) to create encoded image data or use [save](/v2/api/save) to write an image into the filesystem. It's also possible to send a HTTP [response](/v2/api/response) with current image data.

#### Save an image in filesystem

```php
Image::make('foo.jpg')->resize(300, 200)->save('bar.jpg');
```

Read more about [image HTTP responses](/v2/usage/http-response).

### Outputting Image data

- [encode()](/v2/api/encode)
- [save()](/v2/api/save)
- [response()](/v2/api/response)

