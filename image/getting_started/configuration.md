# Configuration

Currently Intervention Image supports two Image processing extensions.

- **GD**
- **Imagick**

Make sure you have one of these installed in your PHP environment, before you start.

### Driver Settings

The configuration file is ```src/config/config.php```. In this file you can define which library should be used by all commands.

> 'driver' => 'imagick'

#### Laravel Configuration

If you're using Laravel, you can pull a configuration file into your application by running the following artisan command.

> $ php artisan config:publish intervention/image

This command copies a configuration file to ```app/config/packages/intervention/image/config.php```, where you can alter the driver settings for you application locally.

### Memory Settings

Image manipulation in PHP is a very memory consuming task. Since most tasks in PHP don't exhaust default memory limits, you have to make sure your PHP configuration is able to allocate enough memory to handle large images.

The following php.ini directives are important.

#### memory_limit

Sets a maximum amount of memory in bytes that a script is allowed to allocate. Resizing a 3000 x 2000 pixel image to 300 x 200 may take up to 32MB memory.

#### upload_max_filesize

If you're planing to upload large images, verify that this setting for the maximum size of file uploads fits your needs.

Read more in the official PHP documentation for:

* [memory_limit](http://www.php.net/manual/en/ini.core.php#ini.memory-limit)
* [upload_max_filesize](http://www.php.net/manual/en/ini.core.php#ini.upload-max-filesize)

It's possible to set these directives in your [php.ini](http://www.php.net/manual/en/ini.core.php) or at runtime with [ini_set](http://www.php.net/manual/en/function.ini-set.php).
