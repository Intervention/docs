---
label: "Palettes & Color Themes"
title: "Palettes & Color Themes"
subtitle: "Extraction of Color Palettes and Themes"
lead: "Extract color palettes with Intervention Image."
sort: 4
---

[TOC]

## Color Palette Extraction

### Dominant Colors

> public ColorExtractor::dominant(int $limit = 8, ?SizeInterface $region = null): PaletteInterface

Extract the most visually prominent colors from an image. This method analyzes the image using a K-Means algorithm and returns the colors that stand out most, regardless of how frequently they appear.

Please note that the limit is the maximum number of colors the palette may contain. The result can contain fewer colors than the specified limit.

#### Parameters

| Name | Type | Description |
| - | - | - |
| limit | int | The maximum number of colors in the extracted palette (Default: 8) |
| region | null or SizeInterface | Limit the color extraction to a region of the image. By default, the entire image. |

<div class="img-centered"><img src="/storage/projects/image/v4/palette_dominant.png"></div>

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

> public ColorExtractor::popular(int $limit = 256, ?SizeInterface $region = null): PaletteInterface

Extract the most frequently used colors from an image. Unlike dominant colors, this method returns colors based on how often they appear in the image pixels. Furthermore, this method uses quantization for images with a large number of colors in order to reduce the colors in a meaningful way. This helps improve performance and prevents the palette from containing too many similar colors.

Please note that the limit is the maximum number of colors the extraction may contain. The result can contain fewer colors than the specified limit.

#### Parameters

| Name | Type | Description |
| - | - | - |
| limit | int | The maximum number of colors in the extracted palette (Default: 256) |
| region | null or SizeInterface | Limit the color extraction to a region of the image. By default, the entire image. |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// read an image
$image = ImageManager::usingDriver(Driver::class)->decode('example.jpg');

// extract the 32 most used colors from the image
$palette = $image->colors()->popular(32);
```

### Color Themes

> public ColorExtractor::theme(Theme|ThemeDefinitionInterface $theme = Theme::VIBRANT_MUTED): ThemeInterface

Extract a color theme from an image. The result provides semantically meaningful colors of the given theme. The default theme provides colors for vibrant, muted, dark, and light variations. If no colors could be found for a theme category in the image, the color swatch property may be `null`.

| Name | Type | Description |
| - | - | - |
| theme | Theme or ThemeDefinitionInterface | The color theme to extract from the image. |

#### Default Theme Properties

- `Intervention\Image\Colors\Themes\VibrantMuted\Theme::$vibrant: ?ColorInterface`
- `Intervention\Image\Colors\Themes\VibrantMuted\Theme::$muted: ?ColorInterface`
- `Intervention\Image\Colors\Themes\VibrantMuted\Theme::$darkVibrant: ?ColorInterface`
- `Intervention\Image\Colors\Themes\VibrantMuted\Theme::$darkMuted: ?ColorInterface`
- `Intervention\Image\Colors\Themes\VibrantMuted\Theme::$lightVibrant: ?ColorInterface`
- `Intervention\Image\Colors\Themes\VibrantMuted\Theme::$lightMuted: ?ColorInterface`

It is possible to create own color theme definitions implementing `Intervention\Image\Interfaces\ThemeDefinitionInterface` and passing the implementation as an argument.

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// read an image
$image = ImageManager::usingDriver(Driver::class)->decode('example.jpg');

// extract color theme from the image
$theme = $image->colors()->theme();

// access individual swatches
$color = $theme->vibrant;  // ColorInterface or null
$color = $theme->muted;  // ColorInterface or null
$color = $theme->darkVibrant;  // ColorInterface or null
$color = $theme->darkMuted;  // ColorInterface or null
$color = $theme->lightVibrant;  // ColorInterface or null
$color = $theme->lightMuted;  // ColorInterface or null

// themes can be transformed into a palette to access all of its methods like sorting
$palette = $theme->toPalette();
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

### Check if a Color is in Palette

> public PaletteInterface::hasColor(ColorInterface $color): bool

Check whether the given color is in the palette.

#### Parameters

| Name | Type | Description |
| - | - | - |
| color | string or ColorInterface | The color to be checked. |

```php
// extract some colors from image 
$palette = $image->colors()->popular()

// check if white is part of the result
$palette->hasColor(Color::rgb(255, 255, 255))

// method also accepts strings
$palette->hasColor('ffffff')

// method also accepts NamedColor::class
$palette->hasColor(NamedColor::WHITE)
```

### Sort Palettes by the Channel Values of their Colors

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

### Count the number of colors in the palette

> public PaletteInterface::count(): int

Get the total number of colors in a palette. This is useful when you need to know how many colors were extracted or remain after filtering operations.

```php
// count colors in extracted palette
$count = $image->colors()->popular()->count();
```

### Filter the colors in the palette

> public PaletteInterface::filter(callable $callback): PaletteInterface

Run callback on each color in the palette and keep only the ones that return `true`.

```php
// filter only grayscale colors
$filtered = $image->colors()->popular()->filter(function (ColorInterface $color): bool {
    return $color->isGrayscale();
});
```

### Map colors in the palette

> public PaletteInterface::map(callable $callback): PaletteInterface

Run a callback on each color in the palette and replace it with the result.

```php
// map colors to semi-transparent variants
$filtered = $image->colors()->popular()->map(function (ColorInterface $color): ColorInterface {
    return $color->withTransparency(.5);
});
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

### Quantize Palettes

> public PaletteInterface::quantizer(int $levels): PaletteInterface

Combine similar colors in the palette to their quantized version according to the given level of quantization.

#### Parameters

| Name | Type | Description |
| - | - | - |
| levels | int | Quantization levels ranging from 256 (for the highest level of detail) to 1 (lowest level). |

```php
// extract popular colors from image
$palette = $image->colors()->popular();

// quantize palette to a lower detail level
$quantizedPalette = $palette->quantize(4);
```

### Reduce Colors in Palettes

> public PaletteInterface::reduce(int $levels): PaletteInterface

Reduce similar colors in the palette by quantization with the given levels of detail but keep original first color values.

#### Parameters

| Name | Type | Description |
| - | - | - |
| levels | int | Quantization levels ranging from 256 (for the highest level of detail) to 1 (lowest level). |

```php
// extract popular colors from image
$palette = $image->colors()->popular();

// quantize palette to a lower detail level but keep original color values
$reducedPalette = $palette->reduce(4);
```
