---
title: "Upgrade Guide"
subtitle: "Upgrade from Intervention Image 3.x to 4.x"
lead: "Learn how to migrate from Intervention Image version 3 to version 4. See what new features are available and what changes have been made in the update."
sort: 3
---

[TOC]

## New Features

### New Decoding Methods

The revised image decoding interface introduces a more transparent approach to
handling image sources. Allowing image sources to be addressed directly instead
of relying on a single universal method. 

- `ImageManagerInterface::decode()`
- `ImageManagerInterface::decodePath()`
- `ImageManagerInterface::decodeBinary()`
- `ImageManagerInterface::decodeBas64()`
- `ImageManagerInterface::decodeDataUri()`
- `ImageManagerInterface::decodeSplFileInfo()`
- `ImageManagerInterface::decodeStream()`

[Read more about decoding methods](/v4/basics/instantiation)

### Exceptions and more detailed Error Messages

At the same time, error and exception messages have been refined to provide
clear, immediate insight into what went wrong. These improvements include a
restructured exception system with a well-defined hierarchy that makes handling
exceptions easier.

[Read more about exceptions](/v4/basics/error-handling)

### Enhancement of the Color System

- Functional [color format](/v4/getting-started/formats#string-format) now supports syntax without comma
- New color generator object `Intervention\Image\Color` to [create and parse](/v4/getting-started/formats#color-formats) more easily
- All colors now have full alpha channel support
- Support for OkLab and Oklch color space
- New enum `NamedColor::class` for css color names.
- New [Color modifier methods](/v4/basics/colors#transforming-colors) `ColorInterface::withTransparency()`, `ColorInterface::withBrightness()`, `ColorInterface::withSaturation` and `ColorInterface::withInversion()`

### More New Features

- DataUri::class
- Alignment::class
- New method `DriverInterface::version()` to check internal version of driver
- Origin::format()
- Support for encoding ICO-Format

## API Changes

### High Impact Changes

It is very likely that you will need to make these adjustments when you update to version 4.

- Intervention Image 4 now requires PHP 8.3.0 or greater.
- `ImageManagerInterface::read()` is now handled by `ImageManagerInterface::decode()` or the [other decode methods](/v4/basics/instantiation)
- `ImageManagerInterface::withDriver()` is now handled by [Image::usingDriver()](/v4/basics/configuration-drivers#create-a-new-image-manager-instance-with-static-helper-methods)
- `ImageManagerInterface::animate()` is replaced by universal [ImageManagerInterface::createImage()](/v4/basics/instantiation#create-images)
- `ImageInterface::toJpeg()` and `ImageInterface::toJpg()` are now handled by i[ImageInterface::encodeUsingFormat()](/v4/basics/image-output#encode-images-using-format)
- `ImageInterface::toPng()` is now handled by [ImageInterface::encodeUsingFormat()](/v4/basics/image-output#encode-images-using-format)
- `ImageInterface::toGif()` is now handled by [ImageInterface::encodeUsingFormat()](/v4/basics/image-output#encode-images-using-format)
- `ImageInterface::toJp2()` and `ImageInterface::toJpeg2000()` are replaced by [ImageInterface::encodeUsingFormat()](/v4/basics/image-output#encode-images-using-format)
- `ImageInterface::toWebp()` is replaced by [ImageInterface::encodeUsingFormat()](/v4/basics/image-output#encode-images-using-format)
- `ImageInterface::toBitmap()` and `ImageInterface::toBmp()` are replaced by [ImageInterface::encodeUsingFormat()](/v4/basics/image-output#encode-images-using-format)
- `ImageInterface::toAvif()` is replaced by [ImageInterface::encodeUsingFormat()](/v4/basics/image-output#encode-images-using-format)
- `ImageInterface::toHeic()` is replaced by [ImageInterface::encodeUsingFormat()](/v4/basics/image-output#encode-images-using-format)
- `ImageInterface::toTiff()` and `ImageInterface::toTif()` are replaced by [ImageInterface::encodeUsingFormat()](/v4/basics/image-output#encode-images-using-format)
- `ImageInterface::encodeByMediaType()` is replaced by [ImageInterface::encodeUsingMediaType()](/v4/basics/image-output)
- `ImageInterface::encodeByPath()` is replaced by [ImageInterface::encodeUsingPath()](/v4/basics/image-output)
- `ImageInterface::encodeByExtension()` is replaced by [ImageInterface::encodeUsingFileExtension()](/v4/basics/image-output)
- `ImageInterface::encodeByExtension()` is replaced by [ImageInterface::encodeUsingFileExtension()](/v4/basics/image-output)
- `ImageInterface::pickColor()` was renamed to [ImageInterface::colorAt()](/v4/basics/colors#read-color-of-a-pixel) and signature has changed, argument `$frame_key` is now `$frame`
- `ImageInterface::pickColors()` was renamed to [ImageInterface::colorsAt()](/v4/basics/colors#read-all-colors-of-certain-pixels-in-animated-images)
- `ImageInterface::pad()` was renamed to [ImageInterface::containDown()](/v4/modifying-images/resizing#contain-resizing-without-upscaling) with different signature
- [ImageInterface::flip()](/v4/modifying-images/effects#mirror-images) now handles both vertical and horizontal mirroring with new `direction` parameter
- `ImageInterface::flop()` was removed. Use [ImageInterface::flip()](/v4/modifying-images/effects#mirror-images) with direction parameter `Direction::HORIZONTAL`
- `ImageInterface::place()` was renamed to [ImageInterface::insert()](/v4/modifying-images/inserting) with a different signature. `offset_x` was renamed to `x` and `offset_y` was renamed to `y`, `opacity` was renamed to `transparency` with `float` instead of `int` and updated argument order
- Signatures of [ImageInterface::drawRectangle()](/v4/modifying-images/drawing), [ImageInterface::drawLine()](/v4/modifying-images/drawing), [ImageInterface::drawEllipse()](/v4/modifying-images/drawing), [ImageInterface::drawCircle()](/v4/modifying-images/drawing), [ImageInterface::drawPolygon()](/v4/modifying-images/drawing) and [ImageInterface::drawBezier()](/v4/modifying-images/drawing) have changed
- Method `ImageInterface::save()` only processes known image file extensions
- `EncodedImageInterface::toDataUri()` now returns `DataUriInterface::class` instead of `string´
- Method `FontInterface::filename()` is replaced by [FontInterface::filepath()](/v4/modifying-images/text-fonts#font-file)
- Method `FontInterface::hasFilename()` is replaced by `FontInterface::hasFile()`
- Method `FontInterface::setFilename()` is replaced by `FontInterface::setFilepath()`
- Method `ColorInterface::convertTo()` was renamed to [ColorInterface::toColorspace()](/v4/basics/colors#transform-colors-between-colorspaces)
- [Config::class](/v4/basics/configuration-drivers#configuration-options) option `blendingColor` was renamed to `backgroundColor`
- Method `ImageInterface::rotate()` rotates clockwise by default.
- `ImageInterface::blendTransparency()` was renamed to [ImageInterface::fillTransparentAreas()](/v4/basics/colors#merge-transparent-areas-with-color) with a different signature allowing (semi) transparent colors
- `ImageInterface::setBlendingColor()` was renamed to [ImageInterface::setBackgroundColor()](/v4/basics/colors#set-the-background-color)
- `ImageInterface::blendingColor()` was renamed to [ImageInterface::backgroundColor()](/v4/basics/colors#read-the-background-color)
- Color value string `transparent` is no longer supported. Use [Intervention\Image\Color::transparent()](/v4/basics/colors#transparency) instead
- Parameter `$prefix` of [ColorInterface::toHex()](/v4/basics/colors#transform-colors-to-hexadecimal-triplet) has now a `boolean` type
- Method `ImageInterface::reduceColors()` has a different type and default value of the argument `$background`. Background defaults now to the configured background color instead of `transparent`.

### Medium Impact Changes

It is possible that you will need to make these adjustments when updating if you have delved deeper into the functions.

- Removed `ColorInterface::toArray()` use `ColorInterface::channels()` and map to desired format
- Removed `ColorInterface::normalize()` use `ColorInterface::channels()` and map to desired format
- Changed default value for `background` to `null` in [ImageInterface::rotate()](/v4/modifying-images/resizing#resize-image-canvas)
- Changed default value for `background` to `null` in [ImageInterface::resizeCanvas()](/v4/modifying-images/resizing#resize-image-canvas)
- Changed default value for `background` to `null` in [ImageInterface::resizeCanvasRelative()](/v4/modifying-images/resizing#resize-image-canvas)
- Changed default value for `background` to `null` in [ImageInterface::contain()](/v4/modifying-images/resizing#contain-resizing-1)
- Changed default value for `background` to `null` in [ImageInterface::containDown()](/v4/modifying-images/resizing#contain-resizing-without-upscaling) former `ImageInterface::pad()`
- Changed default value for `background` to `null` in [ImageInterface::crop()](/v4/modifying-images/resizing#crop-image)
- Signature of [ImageInterface::crop()](/v4/modifying-images/resizing#crop-image) changed from `offset_x` to `x` and `offset_y` to `y`
- Attribute `$per_unit` has change to `$unit` with different signature in `Resolution::class`
- Method `DrawableFactoryInterface::init()` is replaced by `DrawableFactoryInterface::create()`
- Method `DrawableFactoryInterface::create()` is replaced by `DrawableFactoryInterface::drawable()`
- `DriverInterface::handleInput()` is replaced by `DriverInterface::handleImageInput()`, `DriverInterface::handleColorInput()`
- `CollectionInterface::empty()` was renamed to `CollectionInterface::clear()`
- `FontFactory::valign()` was replaced with [FontInterface::align()](/v4/modifying-images/text-fonts)
- `FontInterface::valignment()` was renamed to [FontInterface::verticalAlignment()](/v4/modifying-images/text-fonts)
- `FontInterface::setValignment()` was renamed to [FontInterface::setVerticalAlignment()](/v4/modifying-images/text-fonts)
- `FontInterface::alignment()` was renamed to [FontInterface::horizontalAlignment()](/v4/modifying-images/text-fonts)
- `FontInterface::setAlignment()` was renamed to [FontInterface::setHorizontalAlignment()](/v4/modifying-images/text-fonts)
- `ImageInterface::greyscale()` was renamed to [ImageInterface::grayscale()](/v4/modifying-images/effects#convert-image-to-a-grayscale-version)
- `ColorInterface::isGreyscale()` was renamed to `ColorInterface::isGrayscale()`
- Alpha channel values in `__construct()` or `create()` methods of colors are now defined as float values between `0` and `1`
- `FrameInterface::dispose()` was rename to `FrameInterface::disposalMethod()`
- `FrameInterface::setDispose()` was renamed to `FrameInterface::setDisposalMethod()`
- `ImageManagerInterface::driver()` was removed but you can use the public `$driver` property.
- `FileInterface::toFilePointer()` was renamed to `FileInterface::toStream()`
- Color format string `transparent` is no longer supported. Use[Intervention\Image\Color::transparent()](/v4/basics/colors#transparency) instead

### Low Impact Changes

You will probably only need to make these adjustments when updating if you use
the API extensively and have written your own drivers or modifiers.

- `BlendTransparencyModifer::class` was renamed to `FillTransparentAreasModifier::class`
- `ProfileInterface::class` requires implementation of `::fromPath()`
- `DriverInterface::class` requires implementation of `__construct()`
- `DriverInterface::class` requires implementation of `createCore()`
- Replace `DriverInterface::specialize()` with `DriverInterface::specializeModifier()`, `DriverInterface::specializeAnalyzer()`, `DriverInterface::specializeDecoder()` and `DriverInterface::specializeEncoder()`
- `DriverInterface::handleColorInput()` has null as default
- Signature of `FrameInterface::__construct()` has changed, argument `$offset_left` is know `$offsetLeft` and `$offset_top` is now `$offsetTop`
- Signature of `PixelColorAnalyzer::__construct()` has changed, argument `$frame_key` is know `$frame`
- `ColorChannelInterface::max()` and `ColorChannelInterface::min()` are now static
- Method `ColorChannelInterface::toInt()` was removed use `ColorChannelInterface::value()` instead
- Method `ColorChannelInterface::colorFromNormalized()` requires now a static implementation
- Method `ColorChannelInterface::normalize()` was renamed to `ColorChannelInterface::normalizedValue()`
- `CoreInterface::class` now requires implementation of `CoreInterface::meta()`
- `RectangleResizer::class` was renamed to `Resizer::class`
- `GreyscaleModifier::class` was renamed to `GrayscaleModifier::class`
- `DrawableFactoryInterface::__invoke()` was removed, use `DrawableFactoryInterface::build()` or `DrawableFactoryInterface::drawable()`
- `FontFactory::__invoke()` was removed, use `FontFactory::build()` or `FontFactory::font()`
- `AnimationFactory::__invoke()` was removed, use `AnimationFactory::build()` or `AnimationFactory::animation()`
- `InputHandler::withDecoders()` was renamed to `InputHandler::usingDecoders()`
- Interface `ColorInterface::class` now requires to implement `ColorInterface::withTransparency()`
- Interface `ColorInterface::class` now requires to implement `ColorInterface::alpha()`
- Removed `topLeftPoint()` and `bottomRightPoint()` from `Rectangle::class`
- Removed `ColorChannelInterface::__construct()` from interface
- Removed `DriverInterface::createAnimation()`
- `SizeInterface::relativePositionTo()` was renamed to `SizeInterface::offsetTo()`
- `DrawableInterface` requires the implementation of `factory()` and `adjust()`.
- `ColorProcessorInterface::colorToNative()` was renamed to `ColorProcessorInterface::export()`
- `ColorProcessorInterface::nativeToColor()` was renamed to `ColorProcessorInterface::import()`
