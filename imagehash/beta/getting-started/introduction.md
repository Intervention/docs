---
label: "Introduction"
title: "Intervention ImageHash"
subtitle: "Perceptual Image Hashing for PHP"
lead: "Intervention ImageHash is an extension library to Intervention Image and provides perceptual image hashing with different strategies. Generate compact fingerprints of images and compare them to detect similar or duplicate content."
sort: 0
---

### Features

- Four built-in hashing strategies (Average, Difference, Block, Perceptual)
- Support for GD, Imagick, and libvips drivers
- Seamless integration with Intervention Image processing pipelines
- Hamming distance comparison for similarity detection
- Multiple hash format conversions
- Optional GMP extension support for faster comparisons

### What is Perceptual Image Hashing?

A perceptual hash is a fingerprint of an image based on its visual content. Unlike cryptographic hashes (MD5, SHA1) that change completely with any modification, perceptual hashes remain similar when images look similar. 

This lets you:

- Detect duplicate or near-duplicate images
- Find images that have been resized, compressed, or lightly edited
- Organize and deduplicate image collections
- Implement content moderation and copyright detection


### Code Example

There are two ways to generate image hashes: use the `ImageHasher` class directly, or integrate hashing into an existing Intervention Image pipeline with the `analyze()` method.

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

Read more on how to [install](/beta/getting-started/installation) the package or explore how to [build image hashes](/beta/api/hasher).
