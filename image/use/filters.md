# Image Filters

Image Filters in Intervention Image give you the useful possibility to group image transformations commands into a dedicated object. This object defines which command, in which order and with which arguments should be called on an image instance.

Intervention Image provides the basic ```Intervention\Image\Filters\FilterInterface```, which all filters need to implement.

Once you have created your own filters, you can apply them using the [filter()](/api/filter) method.

#### Applying the demo filter

```php
// init new image instance
$img = Image::make('foo.jpg');

// apply filter
$img->filter(new DemoFilter(45));
```

Take a look at the [example](/api/filter) of the DemoFilter ```src/Intervention/Image/Filters/DemoFilter.php``` which combines a greyscale/pixelate effect.