---
title: "Installation"
subtitle: "Installation with Composer"
lead: "Learn how to install Intervention ImageHash for PHP with Composer and discover how to configure your web server to make the library work perfectly."
sort: 1
---

[TOC]

## Server Requirements

Before you begin with the installation make sure that your server environment supports the following requirements.

- PHP >= 8.3
- Mbstring PHP Extension
- Image Processing PHP Extension

### Image Processing Extension

Your server environment must have at least one PHP image processing extension
installed. Intervention Image currently supports the three most popular.

- [GD Image](https://www.php.net/manual/en/book.image.php)
- [Imagick](https://www.php.net/manual/en/book.imagick.php)
- [libvips](https://www.libvips.org)

## Installation

Install this package with [Composer](https://getcomposer.org).

```bash
composer require intervention/imagehash
```

After the installation you can start using the [image hasher](/beta/api/hasher).
