---
label: "Hash Images"
title: "Building Image Hashes"
subtitle: "Generate Perceptual Image Hashes"
lead: "Learn how to create perceptual image hashes using the ImageHasher class or the Image Analyzer interface."
sort: 0
---

[TOC]

## Building Hashes

Intervention ImageHash provides two approaches for generating perceptual image hashes. You can use the `ImageHasher` class as a standalone hasher, or integrate hashing into an existing Intervention Image processing pipeline using the analyzer interface.

### Using ImageHasher

> public ImageHasher::__construct(string|DriverInterface $driver, StrategyInterface $strategy = new Difference())

The `ImageHasher` class serves as the central starting point for all hashing operations. It requires a driver matching your PHP image extension (GD, Imagick, or libvips) and a hashing strategy.

#### Parameters

| Name | Type | Description |
| - | - | - |
| driver | string or DriverInterface | Image manipulation driver (GD, Imagick, or libvips) |
| strategy | StrategyInterface | Hashing strategy to use (defaults to Difference) |

#### Example

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Difference;

// create hasher with driver and strategy
$hasher = new ImageHasher(new GdDriver(), new Difference());

// generate hash from image path
$hash = $hasher->hash('path/to/image.jpg');
```

### Creating ImageHasher Instances

The `ImageHasher` class provides several static factory methods for creating instances.

#### Create with Static Method

> public static ImageHasher::create(string|DriverInterface $driver, StrategyInterface $strategy = new Difference()): ImageHasher

Create a new hasher instance with the given driver and strategy.

```php
use Intervention\Image\Drivers\Imagick\Driver as ImagickDriver;
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Average;

// create hasher using static method
$hasher = ImageHasher::create(ImagickDriver::class, new Average());
```

#### Create with Driver

> public static ImageHasher::usingDriver(string|DriverInterface $driver): ImageHasher

Create a hasher instance with the specified driver using the default Difference strategy.

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\ImageHasher;

// create hasher with driver (uses default Difference strategy)
$hasher = ImageHasher::usingDriver(GdDriver::class);
```

#### Modify Existing Hasher

You can create new hasher instances from existing ones with modified configuration.

> public ImageHasher::withDriver(string|DriverInterface $driver): ImageHasher

Create a new hasher instance with a different driver, keeping the current strategy.

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\Image\Drivers\Imagick\Driver as ImagickDriver;

$hasher = ImageHasher::usingDriver(GdDriver::class);

// create new hasher with different driver
$imagickHasher = $hasher->withDriver(ImagickDriver::class);
```

> public ImageHasher::withStrategy(StrategyInterface $strategy): ImageHasher

Create a new hasher instance with a different strategy, keeping the current driver.

```php
use Intervention\ImageHash\Strategies\Difference;
use Intervention\ImageHash\Strategies\Perceptual;

$hasher = ImageHasher::usingDriver(GdDriver::class);

// create new hasher with different strategy
$perceptualHasher = $hasher->withStrategy(new Perceptual());
```

### Generate Hashes

> public ImageHasher::hash(mixed $image): HashInterface

Generate a perceptual hash from various image sources. This method accepts the same image sources as Intervention Image's `decode()` method.

#### Parameters

| Name | Type | Description |
| - | - | - |
| image | mixed | Image source (path, binary data, SplFileInfo, base64, data URI, stream, ImageInterface, etc.) |

#### Supported Image Sources

The `hash()` method accepts all [image sources supported by Intervention Image](https://image.intervention.io/v4/basics/instantiation#supported-image-sources):

- Path in filesystem
- Raw binary image data
- `SplFileInfo` object
- Base64 encoded image data
- Data URI string or instance of `DataUriInterface`
- Stream resource
- Instance of `ImageInterface`
- Instance of `EncodedImageInterface`

#### Example

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Difference;

$hasher = new ImageHasher(new GdDriver(), new Difference());

// hash from file path
$hash1 = $hasher->hash('images/photo.jpg');

// hash from binary data
$hash2 = $hasher->hash(file_get_contents('images/photo.jpg'));

// hash from data URI
$hash3 = $hasher->hash('data:image/png;base64,iVBORw0KG...');

// hash from stream resource
$stream = fopen('images/photo.jpg', 'r');
$hash4 = $hasher->hash($stream);
```

### Using the Analyzer Interface

> public AnalyzerInterface::analyze(ImageInterface $image): HashInterface

Instead of using `ImageHasher`, you can use the `Intervention\Image\Image::analyze()` method to integrate hashing into an existing Intervention Image processing pipeline. This is useful when you already have an `ImageInterface` instance from previous image operations.

All hashing strategies implement the `AnalyzerInterface`, so they can be passed directly to the `analyze()` method.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\Strategies\Difference;
use Intervention\ImageHash\Strategies\Average;

// create image manager and load image
$manager = ImageManager::usingDriver(GdDriver::class);
$image = $manager->decodePath('images/photo.jpg');

// apply image modifications
$image->scale(width: 800);
$image->greyscale();

// generate hash using any strategy
$hash1 = $image->analyze(new Difference());
$hash2 = $image->analyze(new Average());
```

This approach is particularly useful when you want to hash an image after processing:

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver as ImagickDriver;
use Intervention\ImageHash\Strategies\Block;

$manager = ImageManager::usingDriver(ImagickDriver::class);

// process and hash image in one pipeline
$hash = $manager->decodePath('images/original.jpg')
    ->resize(1200, 800)
    ->crop(800, 600)
    ->analyze(new Block());
```

