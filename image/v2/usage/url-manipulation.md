# URL based image manipulation
## URL based image manipulation

Within a Laravel application it is possible to use the URL to manipulate images dynamically. The manipulated version of the an image will be stored in the cache and will be loaded directly without resource-intensive GD operation.

An image has to be uploaded only once. All manipulations like resizing or cropping will be handled later, when the file is accessed via a HTTP request like this:

> http://yourhost.com/{route-name}/{template-name}/{file-name}

## Installation

Follow this few easy steps to hook the URL based image manipulation directly into your Laravel application. Once enabled the package generates a dynamic route, which forms the URL mentioned above and uses the caching system specified by your Laravel configuration.

### 1. Install packages
To use URL based image manipulation make sure you have installed the latest versions of both **intervention/image** and **intervention/imagecache** and of course a Laravel application. Refer to the [installation guide](/v2/introduction/installation) of intervention/image and [intervention/imagecache](/v2/usage/cache), if you need help on this. After installation follow a few easy steps to [integrate Intervention Image into Laravel](/v2/getting_started/installation#laravel).

### 2. Publish package configuration
If everything is installed and set **import the configuration file** of the caching package, by running one of the following artisan commands:

#### Publish configuration in Laravel 5

> $ php artisan vendor:publish

#### Publish configuration in Laravel 4

> $ php artisan config:publish intervention/imagecache

You will find the configuration file in your app directory and you may edit it to your needs:

```imagecache.php```

### 3. Name the Route

By default URL based image manipulation is disabled. To enable it, you just need to **define a name for the route** in the configuration file mentioned above. This handle will define the first part of the URI. In this example we name the route ```imagecache```.

```php
'route' => 'imagecache'
```

Essentialy that's it. You may now list all registered routes by entering the following artisan command and check if the new route is listed correctly.

> $ php artisan route:list

### 4. Define source directories

Now you have to let PHP know, where to search for images. You may define as many directories as you like. For example define all the upload directories of your application. The application will search the directories for the <code>filename</code> submited in the route.

```php
'paths' => [
    'storage/uploads/images',
    public_path('img')
]
```

It makes sense to save image files with a unique filename in these directories. Otherwise the package will return the image that is found first.

**Note: For security reasons the route only accepts filenames consisting of the following characters a-z, A-Z, 0-9, - (minus), _ (underscore), / (slash) and . (dot).**

### 5. Templates

The templates are defined as names of [filter classes](/v2/usage/filters), where you can define any manipulation operation. The configuration file comes with three different basic callbacks.

- **small** - 120x90 Pixel
- **medium** - 240x180 Pixel
- **large** - 480x360 Pixel

Feel free to adapt the configuration to your needs. Especially the templates are just basic examples and they are not limited to resizing. You can use every method of ```intervention/image``` available.

```php
'templates' => [
    'small' => 'Intervention\Image\Templates\Small',
    'medium' => 'Intervention\Image\Templates\Medium',
    'large' => 'Intervention\Image\Templates\Large'
]
```

The key of the **templates** array in the configuration file will define the template name as the second part of the url. The value defines the name of the applied filter class. 

#### Accessing the original image file

There are a the following built-in routes, you can use to bypass any template and access the original file directly.

- **original** - Send HTTP response with original image file.
- **download** - Send HTTP response and forces the browser to download the original image file, instead of displaying it.

Just use the name instead of the template name.

> http://yourhost.com/{route-name}/original/{file-name}

#### Filter class example

Take a look at the following example of a template filter class to learn more about [filter classes](/v2/usage/filters) and define your own templates anywhere you like.

```php
<?php

namespace YourApp\Filters;

use Intervention\Image\Image;
use Intervention\Image\Filters\FilterInterface;

class MyFilter implements FilterInterface
{
    public function applyFilter(Image $image)
    {
        return $image->fit(120, 90)->greyscale();
    }
}
```

After the class is loaded you can add it to the templates array in your configuration file.

```php
'templates' => [
    'small' => 'Intervention\Image\Templates\Small',
    'medium' => 'Intervention\Image\Templates\Medium',
    'large' => 'Intervention\Image\Templates\Large',
    'foo' => 'YourApp\Filters\MyFilter'
]
```


#### Custom image quality and format

By default all images requested via URL based image manipulation are generated in the same format as the original with default quality. You can specify custom output settings by passing encoded data in the template class.

```php
public function applyFilter(Image $image)
{
    return $image->fit(120, 90)->encode('jpg', 20);
}
```

### 5. Image Cache Lifetime

Once the route is accessed the first time, the image will be searched, edited according to the template and stored in the cache. So the next time you access the URL, all the GD manipulation is bypassed and the file will come directly from the cache.

You can define a custom lifetime, to define the **minutes** until the next image is created.

```php
'lifetime' => 43200
```