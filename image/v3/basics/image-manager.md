# Image Manager
## Configure Intervention Image

[TOC]

The image manager works as a starting point for all operations. With this
class you determine the used driver by configuration and then call the
methods necessary for instantiation.

## Creating a new image manager instance

### Reading the pixel width

> public ImageManager::__construct(array $options = []): ImageInterface

The instantiation of the image manager configures the entire setup and
specifies the driver. This option is required. The possible values for the
driver are `gd` or `imagick`.

#### Parameters

| Name | Type | Description |
| - | - | - |
| options | array | Image Manager configuration options |

#### Examples

```php
use Intervention\Image\ImageManager;

// create new manager instance with desired driver
$manager = new ImageManager(['driver' => 'imagick']);
```

Read more about the different methods of the image manager in the
[instantiation section](/v3/basics/instantiation)
