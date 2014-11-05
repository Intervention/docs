# Image Formats

The readable image formats depend on the choosen driver (GD or Imagick) and your local configuration. By default Intervention Image currently supports the following major formats.

<table>
    <tr>
        <th>&nbsp;</th>
        <th>JPEG</th>
        <th>PNG</th>
        <th>GIF</th>
        <th>TIF</th>
        <th>BMP</th>
        <th>ICO</th>
        <th>PSD</th>
    </tr>
    <tr>
        <th>GD</th>
        <th>Read/Write</th>
        <th>Read/Write</th>
        <th>Read/Write</th>
        <th>-</th>
        <th>-</th>
        <th>-</th>
        <th>-</th>
    </tr>
    <tr>
        <th>Imagick</th>
        <th>Read/Write</th>
        <th>Read/Write</th>
        <th>Read/Write</th>
        <th>Read/Write</th>
        <th>Read/Write</th>
        <th>Read/Write</th>
        <th>Read/Write</th>
    </tr>
</table>


See documentation of [make](/api/make) method to see how to read image formats from different sources, respectively [encode](/api/encode) and [save](/api/save) to learn how to output images.

---

# Color Formats

Intervention Image supports four ways to define colors for its methods.

## Integer Format
By default the [pickColor](/api/pickColor) method returns the RGB value as integer. You can also pass a color in this format to all other methods.

#### Examples

```php
// pick color and fill image
$color = Image::make('public/foo.jpg')->pickColor(10, 10);
$img->fill($color);

// pass colors of the GD Library
$im = imagecreatefrompng('public/foo.jpg');
$rgb = imagecolorat($im, 10, 15);
$img->fill($rgb);
```


## Array Format

Pass the RGB integers of a color as a PHP array with or without an alpha value between 1 (opaque) and 0 (full transparency).

#### Examples

```php
// color in array format
$img->fill(array(255, 0, 0));

// color in array format with alpha value
$img->fill(array(255, 255, 255, 0.5));
```

## Hexadecimal Format
You can pass colors as a hex triplet used normally in HTML and CSS. It's possible to use six-digit format as well as the shorthand form.

#### Examples

```php
// shorthand hex color
$img->fill('#ccc');

// six-digit hex color
$img->fill('#cccccc');

// works without prefix
$img->fill('cccccc');
```



## RGB &amp; RGBA string format
RGB string values in functional notations are also supported. If you want to include an **alpha** value use the RGBA format like in the following example.

#### Examples

```php
// rgb color value in integer range
$img->fill('rgb(255, 0, 0)');

// rgba color value with alpha
$img->fill('rgba(255, 0, 0, 1)');

// rgba color value with transparent alpha
$img->fill('rgba(0, 0, 0, 0.5)');
```
