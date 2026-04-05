---
title: "Custom Extensions"
subtitle: "Extend Intervention Image"
lead: "Add custom extensions to Intervention Image by streamlining image transformations architecture with own modifiers and analyzers. Learn to group and reuse complex modifications and analyzing logic using custom classes."
sort: 6
---

[TOC]

Intervention Image is highly scalable and can be easily customized to meet your
specific needs. Users can use the `ModifierInterface` and the `AnalyzerInterface` to
organize their own logic into classes in a clear and structured way.

## Custom Modifiers

Modifiers are used to change an image using the logic implemented in the class.

### Implement Custom Modifiers

Intervention Image provides the `Intervention\Image\Interfaces\ModifierInterface`, which all modifiers need to implement. Once you have created your own modifier, you can apply them by using the `Intervention\Image\Image::modify()` method.

The following example shows a custom modifier class that combines a grayscale and a pixelation effect.

```php
use Intervention\Image\Interfaces\ModifierInterface;
use Intervention\Image\Interfaces\ImageInterface;

class MyCustomModifier implements ModifierInterface
{
    public function __construct(protected int $size)
    {
        //
    }

    public function apply(ImageInterface $image): ImageInterface
    {
        $image->pixelate($this->size);
        $image->grayscale();

        return $image;
    }
}
```

### Apply Custom Modifiers

Once the custom modifier is implemented, you can easily apply it to an image instance.

> public Image::modify(ModifierInterface $modifier): ImageInterface

#### Parameters

| Name | Type | Description |
| - | - | - |
| modifier | Intervention\Image\Interfaces\ModifierInterface | Modifier object |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new image instance
$image = ImageManager::usingDriver(Driver::class)->decode('images/example.jpg');

// apply modifier
$image->modify(new MyCustomModifier(25));
```

## Custom Analyzers

Analyzers are designed to extract specific information from an image.

### Implement Custom Analyzers

Intervention Image provides the `Intervention\Image\Interfaces\AnalyzerInterface`, which all analyzers need to implement. With your own analyzer, you can use the `Intervention\Image\Image::analyze()` method to retrieve data.

The following very simple example shows a custom analyzer class that determines the total pixel count of an image.

```php
use Intervention\Image\Interfaces\AnalyzerInterface;
use Intervention\Image\Interfaces\ImageInterface;

class MyCustomAnalyzer implements AnalyzerInterface
{
    public function apply(ImageInterface $image): int
    {
        return $image->width() * $image->height();
    }
}
```

### Apply Custom Analyzers

Once the analyzer is implemented, you can easily apply it to an image instance.

> public Image::analyzer(AnalyzerInterface $analyzer): ImageInterface

#### Parameters

| Name | Type | Description |
| - | - | - |
| analyzer | Intervention\Image\Interfaces\AnalyzerInterface | Analyzer object |

#### Example

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create new image instance
$image = ImageManager::usingDriver(Driver::class)->decode('images/example.jpg');

// apply analyzer
$totalPixels = $image->analyze(new MyCustomAnalyzer()); // 60000
```
