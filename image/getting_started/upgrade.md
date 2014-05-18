# Upgrading from 1.x to 2.x

Although I tried to keep the update to Version 2.x of Intervention Image as compatible as possible, some things have changed. Some methods became redundant, other things have been simplified and therefore had to change. 

In order to keep your application compatible, you need to keep in mind the following changes, when upgrading.

### New Methods

* [filter()](/api/filter) applies filter to an image.

### Changed Method names

* [fit()](/api/fit) replaces the old ```grab()``` method.

### Changed Arguments on methods

* Method [gamma()](/api/gamma) now only accepts one argument for gamma correction. 
* Changed arguments for [resize()](/api/resize) method. Now uses callback to define further options. 
* Changed arguments for [circle()](/api/circle) method. Now uses callback to define further options.
* Changed arguments for [ellipse()](/api/ellipse) method. Now uses callback to define further options.
* Changed arguments for [line()](/api/line) method. Now uses callback to define further options.
* Changed arguments for [rectangle()](/api/rectangle) method. Now uses callback to define further options.

### Dropped methods

* ```open()``` no longer exists, use [make()](/api/make) instead.
* ```raw()``` no longer exists, use [make()](/api/make) instead.
* ```grayscale()``` no longer exists, use [greyscale()](/api/greyscale) instead.