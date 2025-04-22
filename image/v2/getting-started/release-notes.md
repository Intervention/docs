---
title: "Release notes"
subtitle: "List of major changes for every release"
sort: 5
---

These notes cover the major enhancements and changes for every release. For a full change list view the [Commits on Github](https://github.com/Intervention/image/commits/master).

### 2.6.1 July 22nd 2021

- Bugfix

### 2.6.0 July 14th 2021

- Support for encoding JP2 images
- Support for encoding JFIF images
- Support for AV1 Image File Format (AVIF)
- Support for encoding BMP images also with GD driver
- Support for encoding WebP images also with GD driver
- Support for floating point number when passing angles to rotate()
- Support for reading exif data for images not loaded from file
- Bugfix for DataUrl containing newlines inside data
- Changed HTTP version to 1.1 in request when loading images from url
- Fixed PHP 8 compatibility issue
- Fixed compatibility issue with newer Laravel versions
- Fixed issue when converting PNG to WebP
- Minor improvements

### 2.5.1 November 2nd 2019

- Fixed issues with Laravel 6 / PHP 7.3 compatibility

### 2.5.0 June 24th 2019

- Added format parameter to save() method

### 2.4.3 June 1st 2019

- Support for Symfony HTTP response
- Internal code optimization
- Bugfixes

### 2.4.2 May 29th 2018

- Restrict the maximum rotation value to 360 degrees
- Added more MIME types to support more image types
- Added getBoxSize() method for Intervention/Image/Imagick/Font
- Bugfixes

### 2.4.1 September 21st 2017

- Fixed Bug with PNG images losing transparency when cloned with GD driver
- Added getBoxSize() method for imagick fonts
- Internally switched to short array syntax

### 2.4.0 July 4th 2017

- Added WebP support

### 2.3.14 July 3rd 2017

- Support of Laravel 5.5 package Auto-Discovery
- Allow images to be initiated from PSR StreamInterfaces
- Allow parenthesis in filenames when using ImageCache package
- Bugfixes and Improvements
- Phpdoc fixes 

### 2.3.13 April 23rd 2017

- Fixed bug when detecting file names as base64 encoded data
- Phpdoc fixes 

### 2.3.12 April 22nd 2017

- Fixed IDE error
- Fixed bug when reading long file names

### 2.3.11 February 4th 2017

- Added base expection class
- Fixed bug with constant in newer Imagick versions

### 2.3.10 January 12th 2017

- Laravel Lumen 5.4 compatibility

### 2.3.9 January 12th 2017

- Laravel 5.4 compatibility
- Fixed issue when reading image from stream if stream is not seekable
- Added EXIF support to imagick driver without requiring exif extension

### 2.3.8 September 1st 2016

- Bugfixes

### 2.3.7 April 26th 2016

- Minor Improvements

### 2.3.6 February 26th 2016

- Bugfixes

### 2.3.5 January 4th 2016

- Bugfixes

### 2.3.4 November 30th 2015

- Bugfixes

### 2.3.3 November 27th 2015

- Minor improvements

### 2.3.2 August 17th 2015

- Bugfixes

### 2.3.1 July 13th, 2015

- Added ServiceProvider for [Laravel Lumen](http://lumen.laravel.com/)

### 2.3.0 June 29th, 2015

- Changed requirement to PHP >= 5.4
- Added method [stream()](/v2/api/stream).
- Added method [psrResponse()](/v2/api/psr-response).
- Bugfixes

### 2.2.2 June 15th, 2015

- Bugfixes and internal improvements

### 2.2.1 - May 11th, 2015

- Added IoC container alias to enable automatic dependency injection

### 2.2.0 - April 24th, 2015

- Changed internal handling of resizing with Imagick driver
- Introduced cachable Class Templates for [URL based image manipulation](/v2/usage/url-manipulation)
- Bugfixes

### 2.1.3 - March 18th, 2015

- Bugfixes and internal improvements

### 2.1.2 - March 9th, 2015

- Bugfixes and internal improvements

### 2.1.1 - January 29th, 2015

- Bugfixes

### 2.1.0 - January 28th, 2015

- Support for Laravel 5
- Bugfixes

### 2.0.17 - January 5th, 2015

- Added method [iptc()](/v2/api/iptc).

### 2.0.16 - December 22nd, 2014

- Bugfixes

### 2.0.15 - December 15th, 2014

- Exception is thrown, when trying to initialize an image from an URL but file is not found.
- Bugfixes

### 2.0.14 - November 24th, 2014

- Bugfixes

### 2.0.13 - November 10th, 2014

- Added support of writing ICO format with Imagick driver.
- Added support of writing PSD format with Imagick driver.
- Added Content-Length HTTP header field in [response method](/v2/api/response).
- Bugfixes

### 2.0.12 - October 20th, 2014

- Improved phpDoc to make development easier with IDE.
- Added method [filesize()](/v2/api/filesize).
- Added support to decode directly from base64 encoded data.

### 2.0.11 - September 29th, 2014

- PSR-4 autoloading

### 2.0.10 - September 22nd, 2014

- Named [backup](/v2/api/backup) instances
- Bugfixes

### 2.0.9 - September 8th, 2014

- Added optional constraint parameter to widen and heighten
- Added optional position argument to fit command
- Performance improvements

### 2.0.8 - August 25th, 2014

- Added support of writing BMP format with Imagick driver.
- Added possibility to init image from data-url string.
- Bugfixes

### 2.0.7 - August 10th, 2014

- Removed Illuminate dependencies.
- Changed signature of ImageManager constructor. Pass configuration as array.

### 2.0.6 - July 28th, 2014

- Added option to prevent upsizing in [fit()](/v2/api/fit) method.
- Added possibility to draw [polygons](/v2/api/polygon).
- Bugfixes

### 2.0.5 - June 30th, 2014

- Bugfixes

### 2.0.4 - June 16th, 2014

- Added possibility to init directly from Laravel upload object.

### 2.0.3 - June 8th, 2014

- Bugfixes

### 2.0.2 - May 31th, 2014

- [Auto Orientating](/v2/api/orientate)
- Bugfixes

### 2.0.1 - May 25th, 2014

- [Sharpening Images](/v2/api/sharpen)
- Bugfixes

### 2.0.0 - May 18th, 2014

- Additional support of PHP's Imagick extension
- [Image Filter architecture](/v2/usage/filters)
