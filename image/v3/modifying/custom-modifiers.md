# Custom Modifiers
## Group image modifications in classes

You can create your own combinations of image transformations and save them as a custom Image Modifier class.  This modifier defines which command, in which order and with which arguments should be called on an image instance.

Intervention Image provides the simple `Intervention\Image\Interfaces\ModifierInterface`, which all modifiers need to implement.

Once you have created your own modifier, you can apply them by using the `modify()` method.


### Custom modifier implementation

Take a look at this very basic example of a custom modifier class, which combines a greyscale/pixelate effect.

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

### Applying custom modifiers

Once the custom modifier is implemented, you can easily apply it to an image instance.

> public Image::modify(ModifierInterface $modifier): ImageInterface

#### Parameters

| Name | Type | Description |
| - | - | - |
| modifier | Intervention\Image\Interfaces\ModifierInterface | Modifier object  |

#### Example

```php
use Intervention\Image\ImageManager;

// create new image instance
$image = (new ImageManager('imagick'))
        ->make('images/example.jpg');

// apply modifier
$image->apply(new MyCustomModifier(25));
```
