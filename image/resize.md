# Resize Images

* [Resize Images](#resize)
* [Crop Images](#crop)
* [Fit Images](#fit)
* [Resize Boundaries](#resizecanvas)

---

<a name="resize"></a>
## Resize Images

The easiest way to resize an image, is to call [resize()](api/resize) with new values for width and height on an instance. 

```php
Image::make('foo.jpg')->resize(300, 200);
```

It's also possible, just to resize one dimension of an image and keep the other as is. Just resize with ```null``` as the value, you want to keep untouched.

#### Resize Image to given width and keep height

```php
Image::make('foo.jpg')->resize(300, null);
```

As a third parameter, you may optionally provide a callback to constraint certrain parts of the image while resizing. It's possible to lock the image's aspect ratio and/or prevent and unwanted upsizing.


#### Resize Image to given height, keep aspect ratio and prevent from upsizing

```php
Image::make('foo.jpg')->resize(null, 200, function ($constraint) {
    $constraint->aspectRatio();
    $constraint->upsize();
});
```

To keep things clean, there are two shortcut methods [widen()](api/widen) and [heighten()](api/heighten) for proportionally resizing.

#### Resize Images proportionally

```php
Image::make('foo.jpg')->widen(800);
```

```php
Image::make('bar.jpg')->heighten(600);
```

---

<a name="crop"></a>
## Crop Images

Cropping images means to cut out a rectangular part of an image with given width and height. You can call [crop()](api/crop) define optionally x,y coordinates to move the top-left corner of the cutout to a certain position. By default the cutout is centered on the current image.

#### Crop to a centered 300 x 200 pixel area

```php
Image::make('foo.jpg')->crop(300, 200);
```

#### Crop at a certain position

```php
Image::make('foo.jpg')->crop(300, 200, 10, 10);
```

---

<a name="fit"></a>
## Fit Images

To make it even easier Intervention Image comes with the [fit()](api/fit) method. This method combines cropping and resizing in a smart way. [Fit()](api/fit) will find the best fitting aspect ratio of your given width and height on the current image automatically, cut it out and resize it to the given dimension.

#### Fit image to 150 x 150 pixel

```php
Image::make('foo.jpg')->fit(150, 150);
```

---

<a name="resizecanvas"></a>
## Resize Boundaries

If you want to keep the image intact and just resize the image boundaries, you can call the [resizeCanvas()](api/resizecanvas) method.
#### Resize Image Canvas


```php
Image::make('foo.jpg')->resizeCanvas(300, 200);
```

#### Resize Image Canvas with pinned side

It's possible to set an anchor point from where the image resizing is going to happen. For example if you are setting the anchor to ```bottom-left``` this side is pinned and the values of width/height will be added or subtracted to the top-right corner of the image.


```php
Image::make('foo.jpg')->resizeCanvas(300, 200, 'bottom-right');
```


The fourth argument determines if the resizing is going to happen in relative mode. Meaning that the values of width or height will be added or substracted from the current height of the image. The last argument defines a background color for the new areas of the image.

#### Add a 10 pixel red border to the image

```php
Image::make('foo.jpg')->resizeCanvas(10, 10, 'center', true, '#ff0000');
```
