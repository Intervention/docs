# Image Uploads
## Image Uploads

PHP lets people upload files and with Intervention Image you can easily pass an uploaded image to the [make()](/v2/api/make) method. The standard way is to get the temp. file information from the ```$_FILES``` array.

Read more about file uploads in the official [PHP documentation](http://www.php.net/manual/en/features.file-upload.php).

#### Creating Image from File Upload

```php
// read image from temporary file
$img = Image::make($_FILES['image']['tmp_name']);

// resize image
$img->fit(300, 200);

// save image
$img->save('foo/bar.jpg');
```

## Handling image uploads in Laravel

In a Laravel application it is also possible to pass an uploaded file directly to the make method.

#### Creating Image from File Upload in Laravel

```php
// resizing an uploaded file
Image::make(Input::file('photo'))->resize(300, 200)->save('foo.jpg');
```
