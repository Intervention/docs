---
label: "Image Hash Analyzer"
title: "Using AnalyzerInterface to Build Image Hashes"
subtitle: "Generate Perceptual Image Hashes"
lead: "Generate perceptual image hashes with Intervention ImageHash. Two approaches using the Image Analyzer interface in PHP."
sort: 0
---

You can use the `Image::analyze()` method to integrate hashing into an existing Intervention Image processing pipeline or use the `ImageHasher` class as a [standalone hasher](/v1/api/hasher).

## Image Analyzer Method

> public AnalyzerInterface::analyze(ImageInterface $image): mixed

Intervention Image includes an interface for analysis operations that works perfectly for hashing. All [strategies](/v1/api/strategies) implement this interface, so you can pass them directly to the `analyze()` method. This is especially useful when you're already working with an `ImageInterface` instance from previous operations.

All [hashing strategies](/v1/api/strategies) implement the `AnalyzerInterface`, so they can be passed directly to the `analyze()` method.

- `Intervention\ImageHash\Strategies\AverageStrategy`
- `Intervention\ImageHash\Strategies\BlockStrategy`
- `Intervention\ImageHash\Strategies\DifferenceStrategy`
- `Intervention\ImageHash\Strategies\PerceptualStrategy`

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\Strategies\DifferenceStrategy;
use Intervention\ImageHash\Strategies\AverageStrategy;

// create image manager and load image
$manager = ImageManager::usingDriver(GdDriver::class);
$image = $manager->decodePath('images/photo.jpg');

// generate hash using any strategy
$hash1 = $image->analyze(new DifferenceStrategy());
$hash2 = $image->analyze(new AverageStrategy());
```

This approach is particularly useful when you want to hash an image after processing:

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver as ImagickDriver;
use Intervention\ImageHash\Strategies\BlockStrategy;

$manager = ImageManager::usingDriver(ImagickDriver::class);

// process and hash image
$hash = $manager->decodePath('images/original.jpg')
    ->resize(1200, 800)
    ->crop(800, 600)
    ->analyze(new BlockStrategy());
```
