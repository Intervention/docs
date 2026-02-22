---
label: "Error Handling"
title: "Error Handling"
subtitle: "Use the Exception model to handle errors"
lead: "Discover how to use the exception model of Intervention Image to catch and handle different types of er"
sort: 3
---

[TOC]

## Image Exceptions

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
    │   ├── FilePointerException
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
