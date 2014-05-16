# Saving Images

- [Usage](#usage)
- [Image HTTP Responses](#response)

---

## Saving Images

To save the current state of the image object in filesystem just call [save()](api/save). Define optionally a certain path where the image should be saved. The image type will be defined by the file extension. For example if you pass foo.jpg the image will be saved as a JPG file. You can also optionally set the quality of the image file as second parameter.

<a name="usage"></a>
#### Saving an image

```php
Image::make('foo.jpg')->save();
```

#### Saving an image to a desired format

```php
Image::make('foo.jpg')->save('foo.png');
```

#### Saving an image and pass encoding quality

```php
Image::make('foo.jpg')->save('bar.jpg', 65);
```

---

<a name="response"></a>
## Image HTTP Responses

To return an image to the users browser, you can add it directly to a response and it will be returned in JPG format. Don't forget to add a proper content-type.

