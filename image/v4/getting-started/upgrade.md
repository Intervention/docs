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

### Alignment Enum

- Alignment::class

### DataUri Class

- DataUri::class

### More New Features

- DriverInterface::version()
- Origin::format()
- Support for ICO-Format


## API Changes

- Default resolution is now 72 ppi for new images
