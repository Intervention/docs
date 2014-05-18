# Laravel 4 Integration

Intervention Image has optional support for [Laravel 4](http://laravel.com) and comes with a **Service Provider and Facades** for easy integration. After you have installed the Image class correctly, just follow the instructions.

After you have [installed](/getting_started/installation) Intervention Image, open your Laravel config file ```config/app.php``` and add the following lines.

In the ```$providers``` array add the service providers for this package.

> 'Intervention\Image\ImageServiceProvider'

Add the facade of this package to the ```$aliases``` array.

> 'Image' => 'Intervention\Image\Facades\Image'

Now the Image Class will be auto-loaded by Laravel.


## Configuration

By default Intervention Image uses PHP's GD library extension to process all images. If you want to switch to Imagick, you can pull a configuration file into your application by running the following artisan command.

> $ php artisan config:publish intervention/image

This command copies a configuration file to ```app/config/packages/intervention/image/config.php```, where you can alter the driver settings for you application locally.