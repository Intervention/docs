# Reading Images

- [Opening Images](#open)
- [Retrieving Image Information](#infos)
- [Retrieving Exif Data](#exif)

---

<a name="open"></a>
## Opening Images

Intervention Image makes it super easy to read images. The Library takes away any annoying work, the only thing you have to do is to give a file path to the method [make()](api/make).

#### Read image from file

```php
$img = Image::make('foo/bar/baz.jpg');
```

[make()](api/make) is highly variable. It not only reads filepaths but also **URLs, binary image data, GD resources and Imagick objects**.


#### Read image from URL

```php
$img = Image::make('http://example.com/foo.jpg');
```

See more examples to initiate image instances in the [api documentation](api/make).

---

<a name="infos"></a>
## Retrieving Image Information

Once an image is initiated, it's easy to read any information from the object.

#### Get the width of an image

```php
$img = Image::make('foo.jpg')->width();
```

#### Get the height of an image

```php
$img = Image::make('foo.jpg')->height();
```

#### Get the mime type of an image

```php
$img = Image::make('foo.jpg')->mime();
```

---

<a name="exif"></a>
## Retrieving Exif Data

Even Exif meta data is accessible.

#### Read all the Exif meta into an associative array

```php
$data = Image::make('foo.jpg')->exif();
```


#### Read camera model in Exif meta data

```php
$model = Image::make('foo.jpg')->exif('Model');
```
