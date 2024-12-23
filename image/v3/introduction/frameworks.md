# Framework Integration
## Use with your Favorite Framework
Explore how to integrate Intervention Image with Laravel and Symfony frameworks using the official integration packages. Learn to set up configuration files, select drivers (GD or Imagick), and leverage features like auto-orientation, decoding animations, and blending color.

[TOC]

## Laravel

Intervention Image can be easily integrated into a Laravel application with the
[official integration package](https://github.com/Intervention/image-laravel). This package
provides a Laravel service provider, facade and a publishable configuration
file.

Although this integration is not mandatory, it has the advantage of integrating
the configuration centrally in the application.

### Integration

Instead of installing the Intervention Image directly, it is only necessary to integrate
the `intervention/image-laravel` package. The corresponding base libraries are automatically
installed as well.

```bash
composer require intervention/image-laravel
```

Next, add the configuration files to your application using the `vendor:publish` command:

```bash
php artisan vendor:publish --provider="Intervention\Image\Laravel\ServiceProvider"
```

This command will publish the configuration file `image.php` to your `app/config` 
directory. In this file you can set the desired driver for Intervention Image. 
By default the library is configured to use GD library for image processing.

The configuration files looks like this.

```php
return [

    /*
    |--------------------------------------------------------------------------
    | Image Driver
    |--------------------------------------------------------------------------
    |
    | Intervention Image supports “GD Library” and “Imagick” to process images
    | internally. Depending on your PHP setup, you can choose one of them.
    |
    | Included options:
    |   - \Intervention\Image\Drivers\Gd\Driver::class
    |   - \Intervention\Image\Drivers\Imagick\Driver::class
    |
    */

    'driver' => \Intervention\Image\Drivers\Gd\Driver::class,

    /*
    |--------------------------------------------------------------------------
    | Configuration Options
    |--------------------------------------------------------------------------
    |
    | These options control the behavior of Intervention Image.
    |
    | - "autoOrientation" controls whether an imported image should be
    |    automatically rotated according to any existing Exif data.
    |
    | - "decodeAnimation" decides whether a possibly animated image is
    |    decoded as such or whether the animation is discarded.
    |
    | - "blendingColor" Defines the default blending color.
    */

    'options' => [
        'autoOrientation' => true,
        'decodeAnimation' => true,
        'blendingColor' => 'ffffff',
    ]
];
```

You can read more about the different options for
[driver selection](/v3/basics/image-manager#driver-selection), setting options for 
[auto orientation](/v3/modifying/effects#image-orientation-according-to-exif-data), 
[decoding animations](/v3/modifying/animations) and 
[blending color](/v3/basics/colors#transparency).

The integration is now complete and it is possible to access the
[ImageManager](/v3/basics/instantiation) via Laravel's facade.

### Code Examples

#### Reading images from filesystem

```php
use Intervention\Image\Laravel\Facades\Image;

Route::get('/', function () {
    $image = Image::read('images/example.jpg');
});
```

#### Reading image file uploads

```php
use Illuminate\Http\Request;
use Intervention\Image\Laravel\Facades\Image;

Route::post('/upload', function (Request $request) {
    $image = Image::read($request->file('image'));
});
```

## Symfony

Intervention Image can also be integrated into the Symfony framework. A convenient way is to
use the [official integration bundle](https://github.com/Intervention/image-symfony).

Although the use of this integration library is not absolutely mandatory, it
offers a convenient way of central configuration in the Symfony framework.

### Integration

Instead of installing the Intervention Image directly, it is only necessary to require the
bundle package `intervention/image-symfony`. The corresponding dependencies 
are automatically installed as well

```bash
composer require intervention/image-symfony
```

After the successful installation, you can activate the bundle in the file
`config/bundes.php` of your Symfony application by inserting the following 
line into the array.

```php
return [
    // ...
    Intervention\Image\Symfony\InterventionImageBundle::class => ['all' => true],
];
```

Now you can configure the driver of Intervention Image. By default, the bundle
is using the GD library with Intervention Image. This and others options can be
easily configured by creating a file `config/packages/intervention_image.yaml`
and setting the driver class and the default options as follows. 

```yaml
intervention_image:
  driver: Intervention\Image\Drivers\Gd\Driver
  options:
    autoOrientation: true
    decodeAnimation: true
    blendingColor: 'ffffff'
```

First choose between the two supplied drivers `Intervention\Image\Drivers\Gd\Driver` and
`Intervention\Image\Drivers\Imagick\Driver` for example.

Then you can then use the options to determine the behavior of the library. Read more about the different options for
[driver selection](/v3/basics/image-manager#driver-selection), setting options for 
[auto orientation](/v3/modifying/effects#image-orientation-according-to-exif-data), 
[decoding animations](/v3/modifying/animations) and 
[blending color](/v3/basics/colors#transparency).

The integration is now complete and it is possible to access the
[ImageManager](/v3/basics/instantiation) via dependency injection.

### Code Examples

```php
namespace App\Controller;

use Intervention\Image\ImageManager;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;
use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;

class ExampleController extends AbstractController
{
    #[Route('/')]
    public function example(ImageManager $manager): Response
    {
        $image = $manager->read('images/example.jpg');
    }
}
```
