---
label: "Image Hash Analyzer"
title: "Building Image Hashes with Analyzer interface"
subtitle: "Generate Perceptual Image Hashes"
lead: "Learn how to create image hashes using the Image Analyzer interface."
sort: 0
---

Intervention ImageHash provides two approaches for generating perceptual image hashes. You can use the the analyzer interface to integrate hashing into an existing Intervention Image processing pipelin or use the `ImageHasher` class as a [standalone hasher](/beta/api/hasher).

## Image Hash Analyzer

> public AnalyzerInterface::analyze(ImageInterface $image): mixed

Intervention Image already provides an interface for analysis operations. This interface can also be used for hashing. All [strategies](/beta/api/strategies) already implement the analysis interface. This makes it possible to integrate hashing into an existing Intervention Image processing pipeline. This is useful when you already have an `ImageInterface` instance from previous image operations.

All [hashing strategies](/beta/api/strategies) implement the `AnalyzerInterface`, so they can be passed directly to the `analyze()` method.

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
