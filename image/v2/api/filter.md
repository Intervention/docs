# filter — apply filter on image

## Description

> public Intervention\Image\Image filter( Intervention\Image\Filters\FilterInterface $filter )

The method applies custom filter on current image. Filters are bundles of commands which apply combined operations and effects on an image. Any filters must implement the ```Intervention\Image\Filters\FilterInterface```  and call any method that can be applied to an Intervention Image instance.

## Parameters

### filter

Instance of your custom filter. See example of DemoFilter below which combines a greyscale/pixelate effect.

## Return Values
Instance of Intervention\Image\Image

## Examples

```php
// init new image instance
$img = Image::make('foo.jpg');

// apply filter
$img->filter(new DemoFilter(45));
```

#### DemoFilter Example

```php
<?php

namespace Intervention\Image\Filters;

class DemoFilter implements FilterInterface
{
    /**
     * Default size of filter effects
     */
    const DEFAULT_SIZE = 10;

    /**
     * Size of filter effects
     *
     * @var integer
     */
    private $size;

    /**
     * Creates new instance of filter
     *
     * @param integer $size
     */
    public function __construct($size = null)
    {
        $this->size = is_numeric($size) ? intval($size) : self::DEFAULT_SIZE;
    }

    /**
     * Applies filter effects to given image
     *
     * @param  Intervention\Image\Image $image
     * @return Intervention\Image\Image
     */
    public function applyFilter(\Intervention\Image\Image $image)
    {
        $image->pixelate($this->size);
        $image->greyscale();

        return $image;
    }
}
```