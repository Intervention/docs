---
label: "Hash Images"
title: "Building Image Hashes"
subtitle: "Generate Perceptual Image Hashes"
lead: "Learn how to create perceptual image hashes using the ImageHasher class or the Image Analyzer interface. Choose from four different hashing strategies to match your specific use case."
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

## Hashing Strategies

Intervention ImageHash provides four built-in strategies for generating perceptual hashes. Each strategy uses a different algorithm and may perform better or worse depending on your specific use case.

### Difference Strategy

> Intervention\ImageHash\Strategies\Difference

The Difference strategy (also known as dHash or Gradient Hash) generates hashes based on gradients between adjacent pixels. This is the recommended starting point for most applications.

#### How It Works

The strategy resizes the image to 8x9 pixels (or custom size + 1), converts to grayscale, and compares each pixel with its neighbor to the right. Each hash bit is set based on whether the left pixel is brighter than the right pixel.

#### Constructor

```php
public Difference::__construct(int $size = 8)
```

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

#### Best For

- General-purpose image comparison
- Detecting rotated or flipped images
- Good resistance to color changes and minor modifications
- Fast computation

### Average Strategy

> Intervention\ImageHash\Strategies\Average

The Average strategy (also known as aHash or Mean Hash) generates hashes based on the average image color. It's the simplest and fastest hashing algorithm.

#### How It Works

The strategy resizes the image to the specified size (default 8x8), converts to grayscale, calculates the average pixel value, and sets each hash bit based on whether each pixel is above or below the average.

#### Constructor

```php
public Average::__construct(int $size = 8)
```

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

#### Best For

- Fast hashing when performance is critical
- Simple duplicate detection
- Less sensitive to small changes than other strategies
- Lower accuracy but faster computation

### Block Strategy

> Intervention\ImageHash\Strategies\Block

The Block strategy (also known as Blockhash) divides the image into blocks and generates hashes based on block brightness compared to the median. It's based on the algorithm from [blockhash.io](http://blockhash.io).

#### How It Works

The strategy divides the image into blocks, calculates the median brightness across horizontal bands, and sets each hash bit based on whether each block is brighter than the median of its band.

#### Constructor

```php
public Block::__construct(int $size = 16, string $mode = Block::PRECISE)
```

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

#### Best For

- Images with varying dimensions
- Better resistance to scaling and aspect ratio changes
- More accurate than Average for complex images
- Good balance of accuracy and performance

### Perceptual Strategy

> Intervention\ImageHash\Strategies\Perceptual

The Perceptual strategy (also known as pHash) is the original perceptual hash algorithm. It uses a Discrete Cosine Transform (DCT) to identify frequency patterns in the image.

#### How It Works

The strategy resizes the image, converts to grayscale, applies DCT to both rows and columns, extracts the top-left 8x8 DCT coefficients (low frequencies), and compares each coefficient to the average or median.

#### Constructor

```php
public Perceptual::__construct(int $size = 32, string $comparisonMethod = Perceptual::AVERAGE)
```

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

#### Best For

- Highest accuracy for similar image detection
- Resistant to gamma correction and color changes
- Best for finding images with similar visual content
- More computationally intensive than other strategies

## Strategy Comparison

| Strategy | Speed | Accuracy | Use Case | Hash Size (default) |
| - | - | - | - | - |
| **Difference** | Fast | Good | General purpose, recommended | 64 bits |
| **Average** | Fastest | Basic | Simple duplicates, performance-critical | 64 bits |
| **Block** | Medium | Better | Varying dimensions, scaling | 256 bits |
| **Perceptual** | Slower | Best | Highest accuracy, visual similarity | 64 bits |

### Choosing a Strategy

- **Start with Difference** - Good balance of speed and accuracy for most use cases
- **Use Average** - When you need the fastest possible hashing
- **Use Block** - For images with varying sizes or when scaling is common
- **Use Perceptual** - When you need the highest accuracy and can afford the computation cost

Remember that the appropriate hamming distance threshold for "similar" images varies by strategy and use case. Experiment with your specific images to determine the best strategy and threshold.
