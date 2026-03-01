---
title: "Upgrade Guide"
subtitle: "Upgrade from Intervention Image 3.x to 4.x"
lead: "Learn how to migrate from Intervention Image version 3 to version 4. See what new features are available and what changes have been made in the update."
sort: 3
---

[TOC]

## New Features

### New Decoding Methods

The revised image decoding interace introduces a more transparent approach to
handling image sources. Allowing image sources to be addressed directly instead
of relying on a single universal method. 

- ImageManagerInterface::decode()
- ImageManagerInterface::decodePath()
- ImageManagerInterface::decodeBinary()
- ImageManagerInterface::decodeBas64()
- ImageManagerInterface::decodeDataUri()
- ImageManagerInterface::decodeSplFileInfo()
- ImageManagerInterface::decodeStream()

[Read more about decoding methods](/v4/basics/instantiation)

### Exceptions and more detailed Error Messages

At the same time, error and exception messages have been refined to provide
clear, immediate insight into what went wrong. These improvements include a
restructured exception system with a well-defined hierarchy that makes handling
exceptions easier.

[Read more about exceptions](/)

### Enhancement of the Color System

- Function color format now supports syntax without comma
- ColorInterface::create() now accepts functional string color formats as well as single channel values
- All colors now have full alpha channel support
- Support for OkLab color space
- Color::class
- NamedColor::class
- Color modifier methods `ColorInterface::withTransparency()`, `ColorInterface::withBrightness()`, `ColorInterface::withSaturation` and `ColorInterface::withInversion()`

### More New Features

- DataUri::class
- Alignment::class
- DriverInterface::version()
- Origin::format()
- Support for ICO-Format

## API Changes

### High Impact Changes

- `ImageManagerInterface::animate()` is replaced by universal `ImageManagerInterface::createImage()`
- `ImageManagerInterface::read()` is now handled by `ImageManagerInterface::decode*()`
- `ImageManagerInterface::withDriver()` is now handled by `Image::usingDriver()`
- `ImageInterface::toJpeg()` and `ImageInterface::toJpg()` are now handled by `ImageInterface::encodeUsingFormat()`
- `ImageInterface::toPng()` is now handled by `ImageInterface::encodeUsingFormat()`
- `ImageInterface::toGif()` is now handled by `ImageInterface::encodeUsingFormat()`
- `ImageInterface::toJp2()` and `ImageInterface::toJpeg2000()` are replaced by `ImageInterface::encodeUsingFormat()`
- `ImageInterface::toWebp()` is replaced by `ImageInterface::encodeUsingFormat()`
- `ImageInterface::toBitmap()` and `ImageInterface::toBmp()` are replaced by `ImageInterface::encodeUsingFormat()`
- `ImageInterface::toAvif()` is replaced by `ImageInterface::encodeUsingFormat()`
- `ImageInterface::toHeic()` is replaced by `ImageInterface::encodeUsingFormat()`
- `ImageInterface::toTiff()` and `ImageInterface::toTif()` are replaced by `ImageInterface::encodeUsingFormat()`
- `ImageInterface::pickColor()` was renamed to `ImageInterface::colorAt()` and signature has changed, argument `$frame_key` is know `$frame`
- `ImageInterface::pickColors()` was renamed to `ImageInterface::colorsAt()`
- `ImageInterface::pad()` was renamed to `ImageInterface::containDown()` with different signature
- `ImageInterface::place()` was renamed to `ImageInterface::insert()` with a different signature. `offset_x` was renamed to `x` and `offset_y` was renamed to `y` and updated argument order
- Signatures of `ImageInterface::drawRectangle()`, `ImageInterface::drawLine()`, `ImageInterface::drawEllipse()`, `ImageInterface::drawCircle()`, `ImageInterface::drawPolygon()` and `ImageInterface::drawBezier()` have changed
- Method `ImageInterface::save()` only processes known image file extensions
- `EncodedImageInterface::toDataUri()` now returns `DataUriInterface::class` instead of `string´
- Method `FontInterface::filename()` is replaced by `FontInterface::filepath()`
- Method `FontInterface::hasFilename()` is replaced by `FontInterface::hasFile()`
- Method `FontInterface::setFilename()` is replaced by `FontInterface::setFilepath()`
- Method `ColorInterface::convertTo()` was renamed to `ColorInterface::toColorspace()`
- `Config::class` option `blendingColor` was renamed to `backgroundColor`
- Method `ImageInterface::rotate()` rotates clockwise by default.

### Medium Impact Changes

- Removed `ColorInterface::toArray()` use `ColorInterface::channels()` and map to desired format
- Removed `ColorInterface::normalize()` use `ColorInterface::channels()` and map to desired format
- `ImageInterface::blendTransparency()` was renamed to `ImageInterface::fillTransparentAreas()` with a different signature allowing (semi) transparent colors
- `ImageInterface::setBlendingColor()` was renamed to `ImageInterface::setBackgroundColor()`
- `ImageInterface::blendingColor()` was renamed to `ImageInterface::backgroundColor()`
- Changed default value for `background` to `null` in `ImageInterface::rotate()`
- Changed default value for `background` to `null` in `ImageInterface::resizeCanvas()`
- Changed default value for `background` to `null` in `ImageInterface::resizeCanvasRelative()`
- Changed default value for `background` to `null` in `ImageInterface::contain()`
- Changed default value for `background` to `null` in `ImageInterface::containDown()` former `ImageInterface::pad()`
- Changed default value for `background` to `null` in `ImageInterface::crop()`
- Signature of `ImageInterface::crop()` changed from `offset_x` to `x` and `offset_y` to `y`
- Attribute `$per_unit` has change to `$unit` with different signature in `Resolution::class`
- Method `DrawableFactoryInterface::init()` is replaced by `DrawableFactoryInterface::create()`
- Method `DrawableFactoryInterface::create()` is replaced by `DrawableFactoryInterface::drawable()`
- `DriverInterface::handleInput()` is replaced by `DriverInterface::handleImageInput()`, `DriverInterface::handleColorInput()`
- `CollectionInterface::empty()` was renamed to `CollectionInterface::clear()`
- `FontFactory::valign()` was replaced with `FontInterface::align()`
- `FontInterface::valignment()` was renamed to `FontInterface::verticalAlignment()`
- `FontInterface::setValignment()` was renamed to `FontInterface::setVerticalAlignment()`
- `FontInterface::alignment()` was renamed to `FontInterface::horizontalAlignment()`
- `FontInterface::setAlignment()` was renamed to `FontInterface::setHorizontalAlignment()`
- `ImageInterface::greyscale()` was renamed to `ImageInterface::grayscale()`
- `ColorInterface::isGreyscale()` was renamed to `ColorInterface::isGrayscale()`
- Alpha channel values in `__construct()` or `create()` methods of colors are now defined as float values between `0` and `1`
- `FrameInterface::dispose()` was rename to `FrameInterface::disposalMethod()`
- `FrameInterface::setDispose()` was renamed to `FrameInterface::setDisposalMethod()`
- `ImageManagerInterface::driver()` was removed but you can use the public `$driver` property.

### Low Impact Changes

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
