# Image Manager
## Configure Intervention Image

[TOC]

The image manager is the starting point for all operations. With this
class you determine the driver to use and call the methods needed 
for instantiation.

## Create a new image manager instance

> public ImageManager::__construct(string|DriverInterface $driver): ImageInterface

The image manager instantiation configures the entire setup and specifies the
driver. The possible values for the driver are either an instance or a class
name of driver.

Intervention Image is currently shipped with two different drivers. Depending
on your PHP installation, you can choose between GD or Imagick.

- `Intervention\Image\Drivers\Gd\Driver`
- `Intervention\Image\Drivers\Imagick\Driver`

#### Parameters

| Name | Type | Description |
| - | - | - |
| driver | string or DriverInterface | Image Manager driver instance or driver class name |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = new ImageManager(new Driver());

// alternatively create new manager instance by class name
$manager = new ImageManager(Driver::class);
```

## Create a new image manager instance with static helper methods

### Static Constructor

> public static ImageManager::withDriver(string|DriverInterface $driver): ImageInterface

The static helper method acts the same way as the constructor and takes either
a class name or an instance of the driver.

#### Parameters

| Name | Type | Description |
| - | - | - |
| driver | string or DriverInterface | Image Manager driver instance or driver class name |

#### Examples

```php
use Intervention\Image\ImageManager;
use Intervention\Image\Drivers\Imagick\Driver;

// create new manager instance with desired driver
$manager = ImageManager::withDriver(new Driver());

// or create new manager by class name
$manager = ImageManager::withDriver(Driver::class);
```

### Static GD Driver Constructor

> public static ImageManager::gd(): ImageInterface

This static helper methods for GD driver creates a new image manager instance
directly without arguments.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new image manager with gd driver
$manager = ImageManager::gd();
```

### Static Imagick Driver Constructor

> public static ImageManager::imagick(): ImageInterface

This static helper methods takes no arguments and creates a new image manager
instance with Imagick driver directly.

#### Examples

```php
use Intervention\Image\ImageManager;

// create new image manager with gd driver
$manager = ImageManager::imagick();
```

Read more about the different methods of the image manager in the
[instantiation section](/v3/basics/instantiation)
