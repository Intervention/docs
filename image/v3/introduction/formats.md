# Supported formats
## Readable image and color formats

[TOC]

## Image Formats

Intervention Image is able to decode & encode the following image formats. Read more about image encoding in the [output section](/v3/basics/image-output).

### JPEG

JPEG is still the most used image format of the internet. GD and Imagick driver of Intervention Image support encoding & decoding.

```php
// encode and save an image instance in jpeg format
$image->toJpeg()->save('images/example.jpg');
```

### WebP

Encoding & decoding of the WebP graphic format is supported by GD and Imagick driver.

```php
// encode and save an image instance in webp format
$image->toWebp()->save('images/example.webp');
```

### GIF

Since version 3 of Intervention Image there is full support for encoding & decoding of (**animated**) GIF files with GD and Imagick driver.

```php
// encode and save an image instance in gif format
$image->toGif()->save('images/example.gif');
```

### PNG

Encoding & Decoding of PNG formated images is supported by all drivers.

```php
// encode and save an image instance in png format
$image->toPng()->save('images/example.png');
```

### Windows Bitmap

Encoding & Decoding of BMP formated images is supported by all drivers.

```php
// encode and save an image instance in ms windows bitmap format
$image->toBitmap()->save('images/example.bmp');
```

## Color Formats

Intervention Image supports several formats to define colors for its methods.

### Hexadecimal Format

You can pass colors as a hex triplet used normally in HTML and CSS. It's possible to use six-digit format as well as the shorthand form. The leading `#` is optional.

```php
// create new image with red background
$image = (new ImageManager('gd'))->create(300, 200)->fill('b53717');
```
### RGB & RGBA Array Format

Pass the RGB integers of a color as a PHP array with or without an alpha value.

```php
// create new image with half transparent background
$image = (new ImageManager('gd'))->create(300, 200)->fill([15, 20, 255, .5]);
```

### RGB & RGBA String Format

RGB string values in functional notations are also supported. If you want to include an alpha value use the RGBA prefix like in the following example.

```php
// create new image with half transparent background
$image = (new ImageManager('gd'))->create(300, 200)->fill('rgba(15, 20, 255, .5)');
```

### Integer Format

A color is also recognized as an integer by all methods.

```php
// create new image with background color
$image = (new ImageManager('gd'))->create(300, 200)->fill(1829283);
```
