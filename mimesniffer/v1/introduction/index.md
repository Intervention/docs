# Intervention Mime Sniffer
## PHP Media type (MIME) detector

Detecting MIME Content-type in PHP is easy with [mime_content_type](https://www.php.net/manual/en/function.mime-content-type.php) or [Fileinfo](https://www.php.net/manual/en/book.fileinfo.php). But Fileinfo as an extension is sometimes not available on the server. The function `mime_content_type` wants a path to the filesystem as argument and doesn't process if we only have a string value. This package makes it easy to detect the mime types of the content of a given file or string, without any extension dependencies. 

### Code Example

```php
use Intervention\MimeSniffer\MimeSniffer;
use Intervention\MimeSniffer\Types\ImageJpeg;

// detect given string
$sniffer = MimeSniffer::createFromString($content);

// or detect given file
$sniffer = MimeSniffer::createFromFilename('image.jpg');

// returns object of detected type 
$type = $sniffer->getType(); 

$bool = $type->isBinary(); // check if we have binary data
$bool = $type->isImage(); // check if we are dealing with an image
$bool = $type->isVideo(); // check video data was detected
$bool = $type->isAudio(); // check if we have detected audio data
$bool = $type->isArchive(); // check if an archive was detected
$type = (string) $type; // cast type to string (e.g. "image/jpeg")

// you can also check, if the content matches a specific type
$bool = $sniffer->matches(new ImageJpeg);

// or check, if the content matches an array of types
$bool = $sniffer->matches([ImageJpeg::class, ImageGif::class]);

// or check, if the content matches an array of type objects
$bool = $sniffer->matches([new ImageJpeg, $type]);
```
