# Intervention Image

Intervention Image is an open source **PHP image handling and manipulation** library. It provides an easier and expressive way to create, edit, and compose images and supports currently the two most common image processing libraries **GD Library** and **Imagick**.

The class is written to make PHP image manipulating more easier and expressive. No matter if you want to create image thumbnails, watermarks or format large image files Intervention Image helps you to manage every task in an easy way with as little lines of code as possible.

The library follows the FIG standard **PSR-2** to ensure a high level of interoperability between shared PHP code and is fully **unit-tested**.

## Getting started

The library requires at least **PHP version 5.4** and comes with **Laravel Facades and Service Providers** to simplify the optional framework integration.

<p><a href="/getting_started/installation" class="button">Read the installation guide</a><a href="/getting_started/installation#laravel" class="button">Read about Laravel integration</a></p>

---

## Basic Examples

```php
// open an image file
$img = Image::make('public/foo.jpg');

// now you are able to resize the instance
$img->resize(320, 240);

// and insert a watermark for example
$img->insert('public/watermark.png');

// finally we save the image as a new file
$img->save('public/bar.jpg');
```

### Method chaining

Do the same in one line of code.

```php
$img = Image::make('public/foo.jpg')->resize(320, 240)->insert('public/watermark.png');
```

To view more code examples read the documentation on the individual methods [make](/api/make), [resize](/api/resize), [insert](/api/insert), [save](/api/save) and the introduction to [basic usage](/use/basics).
