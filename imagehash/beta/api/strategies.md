---
label: "Hashing Strategies"
title: "Hashing Strategies"
subtitle: "Using different strategies to build image hashes"
lead: "Choose from four different hashing strategies to match your specific use case."
sort: 3
---

[TOC]

## Hashing Strategies

Intervention ImageHash includes four hashing strategies. Each uses a different algorithm with its own strengths depending on your use case.

### Difference Strategy

> public Difference::__construct(int $size = 8)

The Difference strategy (also called dHash or Gradient Hash) generates hashes based on gradients between adjacent pixels. It's the recommended starting point for most use cases.

The strategy resizes images to 8x9 pixels (or custom size + 1), converts to grayscale, then compares each pixel with its right neighbor. Hash bits are set based on whether the left pixel is brighter.

Best suited for:

- General-purpose image comparison
- Detecting rotated or flipped images
- Good resistance to color changes and minor modifications
- Fast computation

#### Parameters

| Parameter | Type | Default | Description |
| - | - | - | - |
| size | int | 8 | Hash size (results in size × size bits) |

#### Example

```php
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Difference;
use Intervention\Image\Drivers\Gd\Driver as GdDriver;

// use default size (8x8 = 64 bits)
$hasher = new ImageHasher(new GdDriver(), new Difference());

// use custom size (16x16 = 256 bits)
$hasher = new ImageHasher(new GdDriver(), new Difference(size: 16));

$hash = $hasher->hash('images/photo.jpg');
```

### Average Strategy

> public Average::__construct(int $size = 8)

The Average strategy (also called aHash or Mean Hash) generates hashes based on average image color. It's the simplest and fastest algorithm.

The strategy resizes images to the specified size (default 8x8), converts to grayscale, calculates the average pixel value, then sets each hash bit based on whether pixels are above or below average.

Best for:

- Fast hashing when performance is critical
- Simple duplicate detection
- Less sensitive to small changes than other strategies
- Lower accuracy but faster computation


#### Parameters

| Parameter | Type | Default | Description |
| - | - | - | - |
| size | int | 8 | Hash size (results in size × size bits) |

#### Example

```php
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Average;
use Intervention\Image\Drivers\Imagick\Driver as ImagickDriver;

// use default size (8x8 = 64 bits)
$hasher = new ImageHasher(new ImagickDriver(), new Average());

// use custom size (12x12 = 144 bits)
$hasher = new ImageHasher(new ImagickDriver(), new Average(size: 12));

$hash = $hasher->hash('images/photo.jpg');
```

### Block Strategy

> public Block::__construct(int $size = 16, string $mode = Block::PRECISE)

The Block strategy (also called Blockhash) divides images into blocks and generates hashes based on block brightness compared to median values. Based on the algorithm from [blockhash.io](http://blockhash.io).

The strategy divides images into blocks, calculates median brightness across horizontal bands, then sets hash bits based on whether each block is brighter than its band median.

Use this for:

- Images with varying dimensions
- Better resistance to scaling and aspect ratio changes
- More accurate than Average for complex images
- Good balance of accuracy and performance

#### Parameters

| Parameter | Type | Default | Description |
| - | - | - | - |
| size | int | 16 | Hash size in bits (must be divisible by 4) |
| mode | string | Block::PRECISE | Computation mode: `Block::PRECISE` or `Block::QUICK` |

#### Constants

- `Block::PRECISE` - Uses weighted blocks for uneven dimensions (more accurate)
- `Block::QUICK` - Uses even, non-overlapping blocks (faster)

#### Example

```php
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Block;
use Intervention\Image\Drivers\Gd\Driver as GdDriver;

// use default settings (16 bits, precise mode)
$hasher = new ImageHasher(new GdDriver(), new Block());

// use custom size with quick mode
$hasher = new ImageHasher(
    new GdDriver(),
    new Block(size: 256, mode: Block::QUICK)
);

// size must be divisible by 4
$hasher = new ImageHasher(new GdDriver(), new Block(size: 64));

$hash = $hasher->hash('images/photo.jpg');
```


### Perceptual Strategy

> public Perceptual::__construct(int $size = 32, string $comparisonMethod = Perceptual::AVERAGE)

The Perceptual strategy (also called pHash) is the original perceptual hash algorithm. It uses Discrete Cosine Transform (DCT) to identify frequency patterns.

The strategy resizes images, converts to grayscale, applies DCT to both rows and columns, extracts the top-left 8x8 DCT coefficients (low frequencies), then compares each coefficient to the average or median.

Best suited for:

- Highest accuracy for similar image detection
- Resistant to gamma correction and color changes
- Best for finding images with similar visual content
- More computationally intensive than other strategies

#### Parameters

| Parameter | Type | Default | Description |
| - | - | - | - |
| size | int | 32 | Initial resize dimension (must be at least 8) |
| comparisonMethod | string | Perceptual::AVERAGE | Comparison method: `Perceptual::AVERAGE` or `Perceptual::MEDIAN` |

#### Constants

- `Perceptual::AVERAGE` - Compare DCT coefficients to average value
- `Perceptual::MEDIAN` - Compare DCT coefficients to median value

#### Example

```php
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Perceptual;
use Intervention\Image\Drivers\Imagick\Driver as ImagickDriver;

// use default settings (size 32, average comparison)
$hasher = new ImageHasher(new ImagickDriver(), new Perceptual());

// use median comparison
$hasher = new ImageHasher(
    new ImagickDriver(),
    new Perceptual(comparisonMethod: Perceptual::MEDIAN)
);

// use larger size for potentially better accuracy
$hasher = new ImageHasher(
    new ImagickDriver(),
    new Perceptual(size: 64)
);

$hash = $hasher->hash('images/photo.jpg');
```
