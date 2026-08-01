---
label: "Image Hasher"
title: "Image Hasher"
subtitle: "Generate Image Hashes with Standalone Image Hasher"
lead: "Create perceptual image hashes using the ImageHasher class in Intervention ImageHash PHP."
sort: 1
---

[TOC]

Intervention ImageHash offers two ways to generate perceptual image hashes: use the `ImageHasher` class as a standalone tool, or integrate hashing into an existing Intervention Image workflow using the [analyzer interface](/beta/api/analyzer).

## Create an ImageHasher

The `ImageHasher` class provides several static factory methods for creating instances.

### Using the Constructor

> public ImageHasher::__construct(string|DriverInterface $driver, StrategyInterface $strategy = new Difference())

The `ImageHasher` class is your starting point for all hashing operations. You need a driver that matches your PHP image extension (GD, Imagick, or libvips) and a hashing strategy.

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

### Using Static Constructor

> public static ImageHasher::create(string|DriverInterface $driver, StrategyInterface $strategy = new Difference()): ImageHasher

Create a new hasher instance with the given driver and strategy.

```php
use Intervention\Image\Drivers\Imagick\Driver as ImagickDriver;
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Average;

// create hasher using static method
$hasher = ImageHasher::create(ImagickDriver::class, new Average());
```

### Using with Driver Constructor

> public static ImageHasher::usingDriver(string|DriverInterface $driver): ImageHasher

Create a hasher instance with the specified driver using the default Difference strategy.

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\ImageHasher;

// create hasher with driver (uses default Difference strategy)
$hasher = ImageHasher::usingDriver(GdDriver::class);
```

## Modify Existing Hasher

You can create new hasher instances from existing ones with modified configuration.

### Update the Driver

> public ImageHasher::withDriver(string|DriverInterface $driver): ImageHasher

Create a new hasher instance with a different driver, keeping the current strategy.

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\Image\Drivers\Imagick\Driver as ImagickDriver;

$hasher = ImageHasher::usingDriver(GdDriver::class);

// create new hasher with different driver
$imagickHasher = $hasher->withDriver(ImagickDriver::class);
```

### Update the Hashing Strategy

> public ImageHasher::withStrategy(StrategyInterface $strategy): ImageHasher

Create a new hasher instance with a different strategy, keeping the current driver.

```php
use Intervention\ImageHash\Strategies\Difference;
use Intervention\ImageHash\Strategies\Perceptual;

$hasher = ImageHasher::usingDriver(GdDriver::class);

// create new hasher with different strategy
$perceptualHasher = $hasher->withStrategy(new Perceptual());
```

## Generate Hashes

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

