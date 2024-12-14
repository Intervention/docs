# Custom Modifiers
## Group Image Modifications in Classes
Streamline image transformations architecture with custom modifiers in Intervention Image. Learn to group and reuse complex modifications using custom classes that implement the ModifierInterface.

All modifier calls can be stored as a combination in a custom image modifier
class. This modifier defines which commands should be applied to an image
instance, in which order, and with which arguments. This makes it easy to
combine complex transformations into a single reusable call.

Intervention Image provides the simple `Intervention\Image\Interfaces\ModifierInterface`, which all modifiers need to implement.

Once you have created your own modifier, you can apply them by using the `modify()` method.

## Custom Modifier Implementation

The following very simple example shows a custom modifier class that combines a grayscale and a pixelate effect.

```php
use Intervention\Image\Interfaces\ModifierInterface;
use Intervention\Image\Interfaces\ImageInterface;

class MyCustomModifier implements ModifierInterface
{
    protected $size;

    public function __construct(int $size)
    {
        $this->size = $size;
    }

    public function apply(ImageInterface $image): ImageInterface
    {
        $image->pixelate($this->size);
        $image->greyscale();

        return $image;
    }
}
```

## Applying Custom Modifiers

Once the custom modifier is implemented, you can easily apply it to an image instance.

> public Image::modify(ModifierInterface $modifier): ImageInterface

#### Parameters

| Name | Type | Description |
| - | - | - |
| modifier | Intervention\Image\Interfaces\ModifierInterface | Modifier object |

#### Example

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = ImageManager::imagick()->read('images/example.jpg');

// apply modifier
$image->modify(new MyCustomModifier(25));
```
