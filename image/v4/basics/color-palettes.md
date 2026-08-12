---
label: "Color Palettes"
title: "Color Palettes"
subtitle: "Handling of Image Colors"
lead: "Extract color palettes with Intervention Image."
sort: 4
---

[TOC]

## Color Palette Extraction

### Dominant Colors

> public ColorExtractor::dominant(int $limit = 8): PaletteInterface

Extract the most visually prominent colors from an image. This method analyzes the image using a K-Means algorithm and returns the colors that stand out most, regardless of how frequently they appear.

Please note that the limit is the maximum number of colors the palette may contain. The result can contain fewer colors than the specified limit.

#### Parameters

| Name | Type | Description |
| - | - | - |
| limit | int | The maximum number of colors in the extracted palette (Default: 8) |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// read an image
$image = ImageManager::usingDriver(Driver::class)->decode('example.jpg');

// extract the 5 most dominant colors from the image
$palette = $image->colors()->dominant(5);
```

### Popular Colors

> public ColorExtractor::popular(int $limit = 256): PaletteInterface

Extract the most frequently used colors from an image. Unlike dominant colors, this method returns colors based on how often they appear in the image pixels. Furthermore, this method uses quantization for images with a large number of colors in order to reduce the colors in a meaningful way. This helps improve performance and prevents the palette from containing too many similar colors.

Please note that the limit is the maximum number of colors the extraction may contain. The result can contain fewer colors than the specified limit.

#### Parameters

| Name | Type | Description |
| - | - | - |
| limit | int | The maximum number of colors in the extracted palette (Default: 256) |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// read an image
$image = ImageManager::usingDriver(Driver::class)->decode('example.jpg');

// extract the 32 most used colors from the image
$palette = $image->colors()->popular(32);
```

### Color Swatches

> public ColorExtractor::swatches(): PaletteInterface

Extract categorized color swatches from an image. This method provides semantically meaningful colors like vibrant, muted, dark, and light variations, useful for creating cohesive color schemes. If no colors could be found for a category in the image, the color swatch values may also be `null`.

#### Available Swatches

- `Intervention\Image\Colors\Swatches::vibrant(): ?ColorInterface`
- `Intervention\Image\Colors\Swatches::muted(): ?ColorInterface`
- `Intervention\Image\Colors\Swatches::darkVibrant(): ?ColorInterface`
- `Intervention\Image\Colors\Swatches::darkMuted(): ?ColorInterface`
- `Intervention\Image\Colors\Swatches::lightVibrant(): ?ColorInterface`
- `Intervention\Image\Colors\Swatches::lightMuted(): ?ColorInterface`

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// read an image
$image = ImageManager::usingDriver(Driver::class)->decode('example.jpg');

// extract color swatches from the image
$swatches = $image->colors()->swatches();

// access individual swatches
$color = $swatches->vibrant();  // ColorInterface or null
$color = $swatches->muted();  // ColorInterface or null
$color = $swatches->darkVibrant();  // ColorInterface or null
$color = $swatches->darkMuted();  // ColorInterface or null
$color = $swatches->lightVibrant();  // ColorInterface or null
$color = $swatches->lightMuted();  // ColorInterface or null
```

## Color Palettes

### Access Individual Colors

Once you have extracted a color palette, you can access individual colors using array notation, helper methods, or by iterating through all colors in the palette.

```php
// extract dominant colors from image
$palette = $image->colors()->dominant();

// access first color (most dominant in this case)
$color = $palette->first();

// access last color (least dominant in this case)
$color = $palette->last();

// palette implement array access
$color = $palette[0];
$color = $palette[1];
$color = $palette[2];

// access colors in iteration
foreach ($palette as $color) {
    $color->toHex();
}
```

### Sorting

> public PaletteInterface::sortByChannel(string|ColorChannelInterface $channel): PaletteInterface

Sort colors in a palette by a specific color channel value. This allows you to arrange colors by properties like hue, saturation, lightness, or any other channel in ascending or descending order.

#### Parameters

| Name | Type | Description |
| - | - | - |
| channel | string or ColorChannelInterface | The color channel whose values are used to sort the colors in the palette. |

```php
use Intervention\Image\Colors\Hsl\Channels\Saturation;

// extract some popular colors from image and sort them by saturation
$palette = $image->colors()->popular(64)->sortByChannel(Saturation::class);

// sort in reverse order
$palette = $image->colors()->popular(64)->sortByChannelDesc(Saturation::class);
```

### Counting

> public PaletteInterface::count(): int

Get the total number of colors in a palette. This is useful when you need to know how many colors were extracted or remain after filtering operations.

```php
// count colors in extracted palette
$count = $image->colors()->popular()->count();
```

### Slicing

> public PaletteInterface::slice(int $offset = 0, ?int $length = null): PaletteInterface

Extract a subset of colors from a palette. This method works like PHP's array_slice function, allowing you to take a specific range of colors from the palette.

```php
// extract some popular colors from image
$palette = $image->colors()->popular();

// take only the first 3 colors
$sliced = $image->colors()->slice(0, 3);
```

### Transform Palette to other Color Spaces

> public PaletteInterface::toColorspace(string|ColorspaceInterface $colorspace): PaletteInterface

Convert all colors in a palette to a different color space. This is helpful when you need to work with colors in formats like CMYK, HSL, or other color models.

#### Parameters

| Name | Type | Description |
| - | - | - |
| colorspace | string or ColorspaceInterface | The color space into which all colors in the palette are converted. |

```php
use Intervention\Image\Colors\Cmyk\Colorspace as Cmyk;

// extract dominant colors from an rgb image
$rgbPalette = $image->colors()->dominant(3);

// convert colors in palette to cmyk
$cmykPalette = $palette->toColorspace(Cmyk::class);
```
