# HTTP Responses

The easiest way to return an image directly to the users browser, is to output the [response()](/api/response) method. It will automatically send HTTP headers according to the currently image and output encoded image data.

#### Sending HTTP response

```php
// create a new image resource
$img = Image::canvas(800, 600, '#ff0000');

// send HTTP header and output image data
echo $img->response('jpg', 70);
```

#### Sending HTTP response manually

```php
// create a new image resource
$img = Image::canvas(800, 600, '#ff0000');

// send HTTP header and output image data
header('Content-Type: image/png');
echo $img->encode('png');
```


Read more about HTTP responses in the [api documentation](/api/response).

---

## HTTP responses in Laravel Applications

In Laravel applications it is almost the same thing, apart from that you can return the method's output directly from your route.

#### Sending HTTP response in Laravel

```php
Route::get('/', function()
{
    $img = Image::canvas(800, 600, '#ff0000');

    return $img->response();
});
```

#### Attaching images to HTTP responses in Laravel Applications

```php
Route::get('/', function()
{
    $img = Image::canvas(800, 600, '#ff0000');

    // create response and add encoded image data
    $response = Response::make($img->encode('png'));

    // set content-type
    $response->header('Content-Type', 'image/png');
    
    // output
    return $response
});
```

