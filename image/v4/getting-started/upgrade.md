---
title: "Upgrade Guide"
subtitle: "Upgrade from Intervention Image 3.x to 4.x"
lead: "Learn how to migrate from Intervention Image version 3 to version 4. See what new features are available and what changes have been made in the update."
sort: 3
---

[TOC]

More than two years after its release, Intervention Image Version 3 is still
going strong. Built on a modern, expandable architecture, it proved to be a
solid foundation that required only minor refinements rather than a complete
overhaul. Over time, a few small issues were identified and carefully resolved,
leading to a series of thoughtful improvements and optimisations. 

Version 4 is therefore less a radical relaunch and more a focused step
forward—making the library more robust, efficient, and user-friendly. That
said, it also introduces some completely new and exciting features that push
Intervention Image even further.

## New Features

### New Decoding Methods

The revised image decoding system introduces a more flexible and transparent
approach to handling image sources. Several decoding methods have been added,
allowing image sources to be addressed directly instead of relying on a single
universal method. 

- ImageManagerInterface::decodeFrom()
- ImageManagerInterface::decodeFromPath()
- ImageManagerInterface::decodeFromBinary()
- ImageManagerInterface::decodeFromBas64()
- ImageManagerInterface::decodeFromDataUri()
- ImageManagerInterface::decodeFromSplFileInfo()
- ImageManagerInterface::decodeFromStream()

[Read more about decoding methods](/)

### Detailed Error Messages

At the same time, error and exception messages have been carefully refined to
provide clear, immediate insight into what went wrong.

These improvements are supported by a completely restructured exception system,
offering a clean, well-defined hierarchy that makes debugging easier and more
intuitive than ever.

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
