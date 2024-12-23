# Image Manager
## Configure Intervention Image
Learn how to create and configure Intervention Image. Discover the image manager, driver options (GD or Imagick), and advanced settings like auto-orientation, animation decoding, and blending colors.

[TOC]

## Create a new Image Manager Instance

> public ImageManager::__construct(string|DriverInterface $driver, mixed ...$options): ImageManager

The image manager is the starting point for all operations. With this class you
determine the driver to use, the configuration options and call the methods
needed for [reading images from different sources](/v3/basics/instantiation#reading-image-sources).

#### Driver Selection

Intervention Image is currently shipped with two different drivers. Depending
on your PHP installation, you can choose between GD or Imagick.

- `Intervention\Image\Drivers\Gd\Driver`
- `Intervention\Image\Drivers\Imagick\Driver`

#### Configuration Options

Optionally, it is possible to pass further detailed configuration parameters to
the constructor that determine the behavior of the library.

These parameters affect how the library handles the [orientation of the image
according to Exif
data](/v3/modifying/effects#image-orientation-according-to-exif-data), whether
[animations are decoded or discarded](/v3/modifying/animations), and what the [default blending
color](/v3/basics/colors#transparency) is.

#### Parameters

| Name | Type | Description |
| - | - | - |
| driver | string or DriverInterface | Image Manager driver instance or driver class name |
| autoOrientation | bool | (optional) Decides whether the image should be automatically aligned based on the Exif data. Default: `true` |
| decodeAnimation | bool | (optional) Whether a possibly animated image is decoded as such or whether the animation is discarded. Default: `true` |
| blendingColor | mixed | (optional) The default blending color. Default: `ffffff` |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver and default configuration
$manager = new ImageManager(new Driver());

// alternatively create new manager instance by class name and default configuration
$manager = new ImageManager(Driver::class);

// same call with configuration options
$manager = new ImageManager(
    Driver::class,
    autoOrientation: false,
    decodeAnimation: true,
    blendingColor: 'ff5500'
);
```

## Create a new Image Manager Instance with Static Helper Methods

### Static Constructor

> public static ImageManager::withDriver(string|DriverInterface $driver, mixed ...$options): ImageManager

The static helper method acts the same way as the constructor and takes either
a class name or an instance of the driver and optionally configuration parameters.

[See possible options for configuration.](/v3/basics/image-manager#create-a-new-image-manager-instance)

#### Parameters

| Name | Type | Description |
| - | - | - |
| driver | string or DriverInterface | Image Manager driver instance or driver class name |
| options | mixed | Optional configuration parameters |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::withDriver(new Driver());

// or create new manager by class name
$manager = ImageManager::withDriver(Driver::class);

// same call with configuration options
$manager = ImageManager::withDriver(
    Driver::class,
    autoOrientation: true,
    decodeAnimation: true,
    blendingColor: 'ff5500'
);
```

### Static GD Driver Constructor

> public static ImageManager::gd(mixed ...$options): ImageManager

This static helper methods for GD driver creates a new image manager instance
directly without arguments or optional configuration options.

[See possible options for configuration.](/v3/basics/image-manager#create-a-new-image-manager-instance)

#### Parameters

| Name | Type | Description |
| - | - | - |
| options | mixed | Optional configuration parameters |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new image manager with gd driver
$manager = ImageManager::gd();

// same call with configuration options
$manager = ImageManager::gd(autoOrientation: false);
```

### Static Imagick Driver Constructor

> public static ImageManager::imagick(mixed ...$options): ImageManager

This static helper methods takes no arguments and creates a new image manager
instance with Imagick driver directly.

[See possible options for configuration.](/v3/basics/image-manager#create-a-new-image-manager-instance)

#### Parameters

| Name | Type | Description |
| - | - | - |
| options | mixed | Optional configuration parameters |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new image manager with imagick driver
$manager = ImageManager::imagick();

// same call with configuration options
$manager = ImageManager::imagick(blendingColor: 'fff000');
```


## Access Image Manager's Driver

> public ImageManager::driver(): DriverInterface

As already described, the Image Manger is created with a driver instance as a
dependency. This function ensures that it can be accessed at a later point in
time.

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Gd\Driver;

// create image manager with driver
$manager = new ImageManager(new Driver());

// access driver from image manager
$driver = $manager->driver();
```




Read more about the different methods of the image manager in the
[instantiation section](/v3/basics/instantiation)

