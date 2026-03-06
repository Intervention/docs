---
label: "Error Handling"
title: "Error Handling"
subtitle: "Use the Exception model to handle errors"
lead: "Discover how to use the exception model of Intervention Image to catch and handle different types of er"
sort: 3
---

[TOC]

## Image Exceptions

If something goes wrong, Intervention Image throws exceptions. For this purpose, a structured hierarchy has been implemented.

All exceptions are extended from a container `Intervention\Image\Exceptions\ImageException` exception class. This makes it possible to
catch all errors in the library in general.

The container class is divided into two types: `LogicException` and
`RuntimeException` indicating and operational failure or that the error can be
fixed by the developer by correcting the code.

These two types are each divided into further sub-branches. This makes it
possible to intercept every type of error and respond accordingly.

```
ImageException
├── LogicException
│   ├── ArgumentException
│   │   └── InvalidArgumentException
│   ├── NotSupportedException
│   └── StateException
│
└── RuntimeException
    ├── MissingDependencyException
    ├── FilesystemException
    │   ├── DirectoryNotFoundException
    │   ├── StreamException
    │   ├── FileNotFoundException
    │   ├── FileNotReadableException
    │   └── FileNotWritableException
    └── DriverException
        ├── AnalyzerException
        ├── ModifierException
        ├── DecoderException
        │   ├── ImageDecoderException
        │   └── ColorDecoderException
        └── EncoderException
```

### LogicExceptions

Exceptions of type `Intervention\Image\LogicException` mean that the API was
not addressed correctly, i.e., there is an error in the end user's code. There
are further sub-types.

#### ArgumentException / InvalidArgumentException

This exceptions are thrown when a argument passed does not match the expected
format. For example, if a negative value is specified for an image width.

#### NotSupportedException

This type of exception indicates that something was requested that lacks
general support. For example, when an image is to be converted to a color space
that is not implemented for the driver.

#### StateException

This type of exception indicates that something is not in the correct state for
the requested operation. For example when you try to decode an image but there
are no decoders in the handler stack.

### RuntimeExceptions

RuntimeException means operational failure. Usually occurs when something
internal goes wrong. See the following sub-types for better understanding.

#### MissingDependencyException

This exception indicates that a dependency is not been met. For example when
you try to use the driver for Imagick but forgot to install the matching PHP
extension.

#### FilesystemException

This extension is thrown when something went wrong in the filesystem. This can
have various causes. For example, a file cannot be read because it does not
exist or there are no permissions to do so. Or a directory cannot be written to
because it does not exist.

There is an exception type for each of these individual cases.

- `Intervention\Image\Exceptions\DirectoryNotFoundException`
- `Intervention\Image\Exceptions\StreamException`
- `Intervention\Image\Exceptions\FileNotFoundException`
- `Intervention\Image\Exceptions\FileNotReadableException`
- `Intervention\Image\Exceptions\FileNotWritableException`

#### DriverException

This exception is thrown when the underlying image extension produces an error.
It is divided into four subtypes, each dealing with a specific driver operation.

- `Intervention\Image\Exceptions\AnalyzerException`
- `Intervention\Image\Exceptions\ModifierException`
- `Intervention\Image\Exceptions\DecoderException`
- `Intervention\Image\Exceptions\EncoderException`
