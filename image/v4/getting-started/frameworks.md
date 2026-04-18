---
title: "Framework Integration"
subtitle: "Integration in your Favorite Framework"
lead: "Explore how to integrate Intervention Image with Laravel and Symfony frameworks using the official integration packages. Learn to set up configuration files, select drivers and leverage features like auto-orientation, decoding animations, and background color."
sort: 2
---

[TOC]

## Laravel

Intervention Image can be easily integrated into a Laravel application with the
[official integration package](https://github.com/Intervention/image-laravel). This package
provides a Laravel service provider, facade, a publishable configuration
file and more.

### Installation

Instead of installing the Intervention Image directly, it is only necessary to integrate
the `intervention/image-laravel` package. The corresponding base libraries are automatically
installed as well.

```bash
composer require intervention/image-laravel
```

### Application-wide Configuration

The extension comes with a global configuration file that is recognized by
Laravel. It is therefore possible to store the settings for Intervention Image
once centrally and not have to define them individually each time you call the
image manager.

The configuration file can be copied to the application with the following command.

```bash
php artisan vendor:publish --provider="Intervention\Image\Laravel\ServiceProvider"
```

This command will publish the configuration file `config/image.php`. Here you
can set the desired driver and its configuration options for Intervention
Image. By default the library is configured to use GD library for image
processing.

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

    'driver' => env('IMAGE_DRIVER', \Intervention\Image\Drivers\Gd\Driver::class),

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
    | - "backgroundColor" Defines the default background & blending color.
    |
    | - "strip" controls if meta data like exif tags should be removed when
    |    encoding images.
    */

    'options' => [
        'autoOrientation' => true,
        'decodeAnimation' => true,
        'backgroundColor' => 'ffffff',
        'strip' => false,
    ]
];
```

You can read more about the different options for
[driver selection](/v4/basics/configuration-drivers#driver-selection), setting options for 
[auto orientation](/v4/modifying-images/effects#image-orientation-according-to-exif-data), 
[decoding animations](/v4/modifying-images/animations) and 
[background color](/v4/basics/colors).

### Static Facade Interface

This package also integrates access to Intervention Image's central entry
point, the `ImageManager::class`, via a static [facade](https://laravel.com/docs/facades). The call provides access to the
centrally configured [image manager](/v4/basics/instantiation) via singleton pattern.

The following code example shows how to read an image from an upload request
the image facade in a Laravel route and save it on disk with a random file
name.

```php
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Route;
use Illuminate\Support\Facades\Storage;
use Illuminate\Support\Str;
use Intervention\Image\Laravel\Facades\Image;

Route::get('/', function (Request $request) {
    $upload = $request->file('image');
    $image = Image::decode($upload)
        ->resize(300, 200);

    Storage::put(
        Str::random() . '.' . $upload->getClientOriginalExtension(),
        $image->encodeUsingFileExtension($upload->getClientOriginalExtension(), quality: 70)
    );
});
```

### Image Response Macro

> image(Image $image, null|string|Format|MediaType|FileExtension $format = null, mixed ...$options)

The package includes a response macro that can be used to elegantly encode an
image resource and convert it to an HTTP response in a single step.

The macro automatically takes care of the HTTP headers in the response that
match the image and the desired output format.

The following code example shows how to read an image from disk apply
modifications and use the image response macro to encode it and send the image
back to the user in one call. Only the first parameter is required.

```php
use Illuminate\Support\Facades\Route;
use Illuminate\Support\Facades\Storage;
use Intervention\Image\Format;
use Intervention\Image\Laravel\Facades\Image;

Route::get('/', function () {
    $image = Image::decodeBinary(Storage::get('example.jpg'))
        ->scale(300, 200);

    return response()->image($image, Format::WEBP, quality: 65);
});
```

## Symfony

Intervention Image can also be integrated into the Symfony framework. A convenient way is to
use the [official integration bundle](https://github.com/Intervention/image-symfony).

Although the use of this integration library is not absolutely mandatory, it
offers a convenient way of central configuration in the Symfony framework.

### Installation

Instead of installing the Intervention Image directly, it is only necessary to require the
bundle package `intervention/image-symfony`. The corresponding dependencies 
are automatically installed as well

```bash
composer require intervention/image-symfony
```

### Application-wide Configuration

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
configured by creating a file `config/packages/intervention_image.yaml` and
setting the driver class and the default options as follows. 

```yaml
intervention_image:
  driver: Intervention\Image\Drivers\Gd\Driver
  options:
    autoOrientation: true
    decodeAnimation: true
    backgroundColor: 'ffffff'
    strip: false
```

First choose between the two supplied drivers `Intervention\Image\Drivers\Gd\Driver` and
`Intervention\Image\Drivers\Imagick\Driver` for example.

Then you can then use the options to determine the behavior of the library. Read more about the different options for
[driver selection](/v4/basics/configuration-drivers#driver-selection), setting options for 
[auto orientation](/v4/modifying-images/effects#image-orientation-according-to-exif-data), 
[decoding animations](/v4/modifying-images/animations) and 
[background color](/v4/basics/colors).

### Dependency Injection

The integration is now complete and it is possible to access the
[ImageManager](/v4/basics/instantiation) via dependency injection.

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
        $image = $manager->decode('images/example.jpg');
    }
}
```

## Tempest

Intervention Image can be used with the [Tempest framework](https://tempestphp.com/). Although the 
use of this integration library is not absolutely mandatory, the [official bundle](https://github.com/Intervention/image-tempest) offers 
a convenient way of a central configuration file.

### Installation

Instead of installing the Intervention Image directly, it is only necessary to require the
bundle package `intervention/image-tempest`. The dependencies are automatically installed as well.

Install the following package in your Tempest application.

```bash
composer require intervention/image-tempest
```

### Application-wide Configuration

You have two configuration options, depending on how much control you need.

#### Basic Configuration

After the installing, you can configure intervention image for the framework. By default, the bundle
is using the GD library with Intervention Image. This and others options can be
configured by setting the image driver in the `.env` file.

```
IMAGE_DRIVER="Intervention\\Image\\Drivers\\Imagick\\Driver"
```

Choose between the two supplied drivers `Intervention\Image\Drivers\Gd\Driver` and `Intervention\Image\Drivers\Imagick\Driver` for example.

#### Detailed Configuration

If you're looking for more in-depth configuration you can skip the `.env` part and publish a more detailed configuration file for Intervention Image by running the following command.

```bash
php tempest install image
```

The call will publish the configuration file `image.config.php` to your local application. Here you can set the driver and more detailed configuration options.

The configuration files looks like this.

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\Image\Tempest\Config as ImageConfig;

use function Tempest\env;

return new ImageConfig(
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
    |   - \Intervention\Image\Drivers\Vips\Driver::class
    */

    driver: env('IMAGE_DRIVER', GdDriver::class),

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
    | - "backgroundColor" Defines the default background & blending color.
    |
    | - "strip" controls if meta data like exif tags should be removed when
    |    encoding images.
    */

    autoOrientation: true,
    decodeAnimation: true,
    backgroundColor: 'ffffff',
    strip: false,
);
```


Then you can then use the options to determine the behavior of the library. Read more about the different options for
[driver selection](/v4/basics/configuration-drivers#driver-selection), setting options for 
[auto orientation](/v4/modifying-images/effects#image-orientation-according-to-exif-data), 
[decoding animations](/v4/modifying-images/animations) and 
[background color](/v4/basics/colors).

### Dependency Injection

The following code example shows how to inject an [image manager](/v4/basics/instantiation) into your controller. The instance has already been automatically configured according to the config file. Of course you are not limited to inject into controller.

```php
use Intervention\Image\Format;
use Intervention\Image\Interfaces\ImageManagerInterface;
use Tempest\Router\Get;
use Tempest\View\View;

use function Tempest\View\view;

final readonly class HomeController
{
    public function __construct(private ImageManagerInterface $imageManager)
    {
        //
    }

    #[Get(uri: '/')]
    public function __invoke(): View
    {
        // process image
        $image = $this->imageManager
            ->decode('./example.jpg')
            ->scale(height: 300)
            ->encodeUsingFormat(Format::WEBP);

        return view('./home.view.php', dataUri: $image->toDataUri());
    }
}
```
