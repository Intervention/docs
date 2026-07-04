---
label: "Introduction"
title: "Intervention ImageHash"
subtitle: "Perceptual image hashing for PHP"
lead: "Intervention ImageHash is an extension library to Intervention Image and provides perceptual image hashing with different strategies. Generate compact fingerprints of images and compare them to detect similar or duplicate content."
sort: 0
---

### What is Perceptual Image Hashing?

A perceptual hash is a fingerprint of an image derived from its visual features. Unlike cryptographic hash functions like MD5 or SHA1, which produce completely different outputs for even minor changes, perceptual hashes are "close" to one another when images are visually similar. This makes them ideal for:

- Detecting duplicate or near-duplicate images
- Finding images that have been resized, compressed, or slightly modified
- Organizing and deduplicating image collections
- Content moderation and copyright detection

### Features

- Four built-in hashing strategies (Average, Difference, Block, Perceptual)
- Support for GD, Imagick, and libvips drivers
- Seamless integration with Intervention Image processing pipelines
- Hamming distance comparison for similarity detection
- Multiple hash format conversions (hex, bits, bytes)
- Optional GMP extension support for faster comparisons

### Code Example

The library provides two approaches for generating image hashes. You can use the `ImageHasher` class directly or integrate hashing into an existing Intervention Image pipeline using the `analyze()` method.

#### Using ImageHasher

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Difference;

// create hasher with driver and strategy
$hasher = new ImageHasher(new GdDriver(), new Difference());

// generate hash from image path
$hash = $hasher->hash('path/to/image.jpg');

// convert hash to hexadecimal format
echo $hash->toHex(); // "8f9e9d8b0f0f1f07"
```

#### Using Image Analyzer

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\Strategies\Difference;

// create image manager and decode image
$image = ImageManager::usingDriver(GdDriver::class)
    ->decodePath('path/to/image.jpg');

// generate hash using analyze method
$hash = $image->analyze(new Difference());
```

Read more on how to [install](/beta/getting-started/installation) the package or explore how to [build image hashes](/beta/api/hashing).
