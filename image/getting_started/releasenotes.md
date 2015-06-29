# Release notes

These notes cover the major enhancements and changes for every release. For a full change list view the [Commits on Github](https://github.com/Intervention/image/commits/master).

### 2.3.0 June 29th, 2015

- Changed requirement to PHP >= 5.4
- Added method [stream()](/api/stream).
- Added method [psrResponse()](/api/psrResponse).
- Bugfixes

### 2.2.2 June 15th, 2015

- Bugfixes and internal improvements

### 2.2.1 - May 11th, 2015

- Added IoC container alias to enable automatic dependency injection

### 2.2.0 - April 24th, 2015

- Changed internal handling of resizing with Imagick driver
- Introduced cachable Class Templates for [URL based image manipulation](/use/url)
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

- Added method [iptc()](/api/iptc).

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
- Added Content-Length HTTP header field in [response method](/api/response).
- Bugfixes

### 2.0.12 - October 20th, 2014

- Improved phpDoc to make development easier with IDE.
- Added method [filesize()](/api/filesize).
- Added support to decode directly from base64 encoded data.

### 2.0.11 - September 29th, 2014

- PSR-4 autoloading

### 2.0.10 - September 22nd, 2014

- Named [backup](/api/backup) instances
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

- Added option to prevent upsizing in [fit()](/api/fit) method.
- Added possibility to draw [polygons](/api/polygon).
- Bugfixes

### 2.0.5 - June 30th, 2014

- Bugfixes

### 2.0.4 - June 16th, 2014

- Added possibility to init directly from Laravel upload object.

### 2.0.3 - June 8th, 2014

- Bugfixes

### 2.0.2 - May 31th, 2014

- [Auto Orientating](/api/orientate)
- Bugfixes

### 2.0.1 - May 25th, 2014

- [Sharpening Images](/api/sharpen)
- Bugfixes

### 2.0.0 - May 18th, 2014

- Additional support of PHP's Imagick extension
- [Image Filter architecture](/use/filters)
