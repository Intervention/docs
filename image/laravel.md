# Laravel 4 Integration

Intervention Image has optional support for [Laravel 4](http://laravel.com) and comes with a **Service Provider and Facades** for easy integration. After you have installed the Image class correctly, just follow the instructions.

Open your Laravel config file ```config/app.php``` and add the following lines.

In the ```$providers``` array add the service providers for this package.

> 'Intervention\Image\ImageServiceProvider'

Add the facade of this package to the ```$aliases``` array.

> 'Image' => 'Intervention\Image\Facades\Image'

Now the Image Class will be auto-loaded by Laravel.

## Examples

### Handling images from file uploads

It's possible to pass an uploaded file directly to the make method.

```php
// resizing an uploaded file
Image::make(Input::file('photo')->getRealPath())->resize(300, 200)->save('foo.jpg');
```

### Attaching images to HTTP responses

To return an image directly, you can add it directly to a response and it will be returned in **JPG format**. Don't forget to add a proper ```content-type```.

```php
// create/resize image from file
$image = Image::make('public/foo.png')->resize(300, 200);

// return response
return Response::make($image, 200, array('Content-Type' => 'image/jpeg'));
```

If you want to attach other formats than the default JPG, use the [encode](api/encode) method.

```php
// create/resize image from file
$image = Image::make('public/foo.jpg')->resize(300, 200);

// create response and add formated image
$response = Response::make($image->encode('png'));

// set content-type
$response->header('Content-Type', 'image/png');

// et voila
return $response;
```

It's also possible to use the shortcut method [response](api/response) to create the HTTP response automatically.

```php
Route::get('/', function()
{
    $img = Image::make('public/foo.jpg');

    return $img->response();
});
```
