---
title: "Upgrade Guide"
subtitle: "Upgrade from Intervention Image 2.x to 3.x"
lead: "Learn how to quickly migrate from Intervention Image version 2 to version 3. See what new features are available and what changes have been made in the update."
sort: 3
---

[TOC]

## New Features

Intervention Image 3 has been rewritten from the ground up with very little code carried
over from the previous version. This means a more modern and sophisticated
architecture and API that takes advantage of the modern features of PHP 8+.
There are a few key features that further improve the library.

- [Support of animated GIF with GD and Imagick drivers](/v3/basics/instantiation#creating-animations)
- [Configurable Image Manager](/v3/basics/configuration-drivers#create-a-new-image-manager-instance)
- [Support for colorspaces](/v3/basics/colors#colorspaces)
- [Support for text wrapping in font system](/v3/modifying-images/text-fonts)
- [Support for line height in font system](/v3/modifying-images/text-fonts)
- [Object for encoded images](/v3/basics/image-output#handling-of-encoded-image-data)

## API Changes

- [canvas()](/v2/api/canvas) is now handled by [create()](/v3/basics/instantiation#creating-new-images)
- [circle()](/v2/api/circle) is now handled by [drawCircle()](/v3/modifying-images/drawing#drawing-a-circle)
- [crop()](/v2/api/crop) still exists but has a new [signature](/v3/modifying-images/resizing#crop-image)
- [ellipse()](/v2/api/ellipse) is now handled by [drawEllipse()](/v3/modifying-images/drawing#drawing-ellipses)
- [line()](/v2/api/line) has been replaced by [drawLine()](/v3/modifying-images/drawing#drawing-a-line)
- [pixel()](/v2/api/pixel) is handled by [drawPixel()](/v3/modifying-images/drawing#drawing-a-pixel)
- [encode()](/v2/api/encode) still exists but has a new [signature](/v3/basics/image-output#encoding-images)
- [exif()](/v2/api/exif) is now handled by [exif()](/v3/basics/meta-information#exif-information) with a different signature
- [fill()](/v3/modifying-images/drawing#fill-images-with-color) currently only supports color values
- [filter()](/v2/api/filter) is now handled by [modify()](/v3/modifying-images/custom-modifiers)
- [flip()](/v2/api/flip) still exists but has a new signature and is handled by [flip()](/v3/modifying-images/effects#mirror-image-horizontally) and [flop()](/v3/modifying-images/effects#mirror-image-vertically)
- [insert()](/v2/api/insert) has been replaced by [place()](/v3/modifying-images/inserting)
- [make()](/v2/api/make) has been replaced by [read()](/v3/basics/instantiation#reading-image-sources)
- [mime()](/v2/api/make) is now handled by an [encoded image](/v3/basics/image-output#handling-of-encoded-image-data) only
- [pickColor()](/v2/api/pick-color) has a different signature without format which is handled by the [color class](/v3/basics/meta-information#reading-colors-of-certain-pixels)
- [polygon()](/v2/api/polygon) is handled by [drawPolygon()](/v3/modifying-images/drawing#drawing-a-polygon)
- [rectangle()](/v2/api/rectangle) is handled by [drawRectangle()](/v3/modifying-images/drawing#drawing-a-rectangle)
- [text()](/v2/api/text) still exists but has a new [signature](/v3/modifying-images/text-fonts)
- [resizeCanvas()](/v2/api/resize-canvas) still exists but has a new [signature](/v3/modifying-images/resizing)
- [limitColors()](/v2/api/limit-colors) is handled by [reduceColors](/v3/modifying-images/effects)
- [trim()](/v2/api/trim) exists as of version `3.6`, but works differently and [automatically removes border areas](/v3/modifying-images/resizing#trim-image) of the image with similar colors
- [getCore()](/v2/api/get-core) is replaced with [core()](/v3/modifying-images/advanced) but behaves completely differently
- [orientate()](/v2/api/orientate) is handled by [orient()](/v3/modifying-images/effects#image-orientation-according-to-exif-data) and is applied automatically by default ([configurable](/v3/basics/configuration-drivers))
- [resize()](/v2/api/resize) still exists but has a different signature without a callback. The constraint option combinations are handled in a different way by the following other methods [resizeDown()](/v3/modifying-images/resizing#resize-without-exceeding-the-original-size), [scale()](/v3/modifying-images/resizing#scale-images) and [scaleDown()](/v3/modifying-images/resizing#scale-images-but-do-not-exceed-the-original-size)
- [widen()](/v2/api/widen) and [heighten()](/v2/api/heighten) are replaced by calling [scale()](/v3/modifying-images/resizing#scale-images) and [scaleDown()](/v3/modifying-images/resizing#scale-images-but-do-not-exceed-the-original-size) with named arguments
- [fit()](/v2/api/fit) is replaced by [cover()](/v3/modifying-images/resizing#fitted-image-resizing) and [coverDown()](/v3/modifying-images/resizing#fitted-resizing-without-exceeding-the-original-size)

## Removed Features

- [interlace()](/v2/api/interlace) no longer exists and is handle by [encoder options](/v3/basics/image-output).
- [backup()](/v2/api/backup) and [reset()](/v2/api/reset) no longer exist but the functionality can be achieved more easily with [native object cloning](https://www.php.net/manual/en/language.oop5.cloning.php)
- [basepath()](/v2/api/base-path) no longer exists
- [cache()](/v2/api/cache) no longer exists
- [filesize()](/v2/api/filesize) no longer exists
- [iptc()](/v2/api/iptc) no longer exists
- [mask()](/v2/api/mask) no longer exists
- [opacity()](/v2/api/opacity) no longer exists
- [psrResponse()](/v2/api/psr-response) no longer exists
- [response()](/v2/api/response) no longer exists
- [stream()](/v2/api/stream) no longer exists but you may use [toFilePointer()](/v3/basics/image-output#transform-encoded-image-to-file-pointer)
- [destroy()](/v2/api/destroy) no longer exists but you can use PHP's own functions, such as [unset](https://www.php.net/manual/en/function.unset), to free memory

## Other Changes

- The [caching library](https://packagist.org/packages/intervention/imagecache)
  of Intervention Image 2 is not supported by the new version. 

- The service providers for the Laravel framework were removed to avoid a dependency to
  the framework and to highlight Intervention Image rather framework agnostic,
  which it always was. However, there is an [official package for Laravel integration](https://github.com/Intervention/image-laravel)

- It is no longer possible to create images from an URI directly. The data must
  first be loaded by a dedicated HTTP client and then passed to the image
  library. Intervention Image is not responsible for HTTP client operations.

- It is no longer possible to pass color values as array.

- If you use the Laravel framework and a configuration file, it is necessary to
  adjust the `driver` settings option. In version 2, the driver was configured via a
  string such as `gd` or `imagick`. In version 3, this is done via the class
  name of the driver like `Intervention\Image\Drivers\Imagick\Driver`  or
  `Intervention\Image\Drivers\Gd\Driver`. Read [further details about
  configuration](/v3/basics/configuration-drivers) and [Laravel Integration](/v3/introduction/frameworks#laravel)
