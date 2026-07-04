---
label: "Hash Object"
title: "Working with Hash Objects"
subtitle: "Compare, Convert and Store Image Hashes"
lead: "Learn how to work with Hash objects. Compare hashes to detect similar images, convert between different formats, and reconstruct hashes from stored values."
sort: 1
---

[TOC]

## Overview

When you generate an image hash using any hashing strategy, you receive a `Hash` object implementing the `HashInterface`. This object represents a perceptual fingerprint of the image and provides methods for comparison, conversion, and serialization.

The `Hash` object is:
- **Immutable** - Once created, it cannot be modified
- **Serializable** - Implements `JsonSerializable` and `Stringable`
- **Comparable** - Can calculate hamming distance to other hashes

## Comparing Hashes

Perceptual hashes can be compared to determine how similar two images are. The library uses the Hamming distance algorithm to count the number of differing bits between two hashes.

### Calculate Distance

> public Hash::distance(HashInterface $hash): int

Calculate the Hamming distance between two hashes. The distance represents the number of bits that differ between the hashes. A lower distance indicates more similar images.

#### Parameters

| Name | Type | Description |
| - | - | - |
| hash | HashInterface | The hash to compare against |

#### Return Value

Returns an integer representing the number of differing bits. A distance of `0` means the hashes are identical.

Both hashes must have the same bit length for comparison. If the GMP extension is available, it uses `gmp_hamdist()` for faster comparison. Without GMP, falls back to array comparison (still fast, but slightly slower)


#### Example

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Difference;

$hasher = new ImageHasher(new GdDriver(), new Difference());

// generate hashes for two images
$hash1 = $hasher->hash('images/photo1.jpg');
$hash2 = $hasher->hash('images/photo2.jpg');

// calculate hamming distance
$distance = $hash1->distance($hash2); // 3

// lower distance = more similar
if ($distance < 10) {
    echo "Images are very similar";
} elseif ($distance < 20) {
    echo "Images are somewhat similar";
} else {
    echo "Images are different";
}
```

### Check Equality

> public Hash::equals(HashInterface $hash, int $leeway = 0): bool

Determine if two hashes are equal within an optional leeway distance. This is a convenience method that compares the distance to a threshold.

#### Parameters

| Name | Type | Description |
| - | - | - |
| hash | HashInterface | The hash to compare against |
| leeway | int | Maximum allowed distance to still consider equal (default: 0) |

#### Return Value

Returns `true` if the distance is less than or equal to the leeway, `false` otherwise.

#### Example

```php
use Intervention\Image\Drivers\Gd\Driver as GdDriver;
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Difference;

$hasher = new ImageHasher(new GdDriver(), new Difference());

$hash1 = $hasher->hash('images/original.jpg');
$hash2 = $hasher->hash('images/slightly_modified.jpg');

// check for exact match
$exact = $hash1->equals($hash2); // false

// check with leeway for minor differences
$similar = $hash1->equals($hash2, leeway: 5); // true

// practical example: find duplicates with tolerance
$tolerance = 10;
if ($hash1->equals($hash2, leeway: $tolerance)) {
    echo "Images are duplicates or very similar";
}
```

## Converting Hashes

Hash objects can be converted to various formats for storage, transmission, or display. All conversions are lossless and can be reversed.

### Convert to Hexadecimal

> public Hash::toHex(): string

Convert the hash to a hexadecimal string. This is the most common format for storage and is used as the default string representation.

#### Example

```php
use Intervention\ImageHash\Hash;

$hash = $hasher->hash('images/photo.jpg');

$hex = $hash->toHex();
echo $hex; // "8f9e9d8b0f0f1f07"

// hash objects cast to string automatically use hex format
echo (string) $hash; // "8f9e9d8b0f0f1f07"
echo "$hash";        // "8f9e9d8b0f0f1f07"
```

### Convert to Bits

> public Hash::toBits(): string

Convert the hash to a binary string representation (concatenated "0" and "1" characters).

#### Example

```php
use Intervention\ImageHash\Hash;

$hash = $hasher->hash('images/photo.jpg');

$bits = $hash->toBits();
echo $bits; // "1000111110011110100111011000101100001111000011110001111100000111"

// useful for debugging or understanding the hash structure
$bitLength = strlen($bits); // 64
```

### Convert to Bytes

> public Hash::toBytes(): string

Get the raw byte string representation of the hash. This is the internal storage format.

#### Example

```php
use Intervention\ImageHash\Hash;

$hash = $hasher->hash('images/photo.jpg');

$bytes = $hash->toBytes();

// useful for binary storage or transmission
file_put_contents('hash.bin', $bytes);
```

### Convert to Base64

> public Hash::toBase64(): string

Convert the hash to a Base64-encoded string. Useful for embedding in JSON, URLs, or text-based protocols.

#### Example

```php
use Intervention\ImageHash\Hash;

$hash = $hasher->hash('images/photo.jpg');

$base64 = $hash->toBase64();
echo $base64; // "j56diwoPHwc="

// useful for APIs or JSON responses
$response = [
    'image_id' => 123,
    'hash' => $hash->toBase64(),
];
```

### Get Bit Length

> public Hash::bitLength(): int

Get the total number of bits in the hash. Different strategies and configurations produce different bit lengths.

#### Example

```php
use Intervention\ImageHash\ImageHasher;
use Intervention\ImageHash\Strategies\Difference;
use Intervention\ImageHash\Strategies\Block;

$hasher = ImageHasher::usingDriver(GdDriver::class);

// different strategies have different bit lengths
$diff8 = $hasher->withStrategy(new Difference(size: 8))->hash('image.jpg');
echo $diff8->bitLength(); // 64 (8x8)

$diff16 = $hasher->withStrategy(new Difference(size: 16))->hash('image.jpg');
echo $diff16->bitLength(); // 256 (16x16)

$block = $hasher->withStrategy(new Block(size: 16))->hash('image.jpg');
echo $block->bitLength(); // 256
```

## Parsing Hashes

If you've previously stored a hash value, you can reconstruct a `Hash` object using static factory methods. This is useful for comparing newly generated hashes against previously stored ones.

### Parse from Hexadecimal

> public static Hash::fromHex(string $hex): Hash

Create a Hash object from a hexadecimal string. The method validates the input and throws `InvalidArgumentException` if the input can not be parsed to a hash.

#### Parameters

| Name | Type | Description |
| - | - | - |
| hex | string | Hexadecimal string (must be even length, at least 2 characters) |

#### Example

```php
use Intervention\ImageHash\Hash;

// reconstruct hash from stored hex value
$storedHex = "8f9e9d8b0f0f1f07";
$hash = Hash::fromHex($storedHex);

// compare with newly generated hash
$newHash = $hasher->hash('images/uploaded_photo.jpg');
$distance = $hash->distance($newHash);

if ($distance < 10) {
    echo "This image already exists in the database";
}
```

### Parse from Bits

> public static Hash::fromBits(string|array $bits): Hash

Create a Hash object from a binary string or array of bit values. The method accepts bits in multiple formats:

- String of "0" and "1" characters: `"10011010"`
- Array of integers: `[1, 0, 0, 1, 1, 0, 1, 0]`
- Array of booleans: `[true, false, false, true]`
- Array of strings: `["1", "0", "0", "1"]`

The method validates the input and throws `InvalidArgumentException` if the bits can not be converted to a image hash.

#### Parameters

| Name | Type | Description |
| - | - | - |
| bits | string or array | Binary string (e.g., "10011010") or array of bits (e.g., [1, 0, 0, 1]) |

#### Example

```php
use Intervention\ImageHash\Hash;

// from binary string
$hash1 = Hash::fromBits("1000111110011110100111011000101100001111000011110001111100000111");

// from array of integers
$hash2 = Hash::fromBits([1, 0, 0, 0, 1, 1, 1, 1, 1, 0, 0, 1, 1, 1, 1, 0]);

// from array of booleans
$hash3 = Hash::fromBits([true, false, false, false, true, true, true, true]);

// all formats can be compared
echo $hash1->toHex();
```

### Parse from Bytes

> public static Hash::fromBytes(string $bytes): Hash

Create a Hash object from a raw byte string.

#### Parameters

| Name | Type | Description |
| - | - | - |
| bytes | string | Raw byte string (minimum 1 byte) |

#### Example

```php
use Intervention\ImageHash\Hash;

// load from binary file
$bytes = file_get_contents('hash.bin');
$hash = Hash::fromBytes($bytes);

// compare with new hash
$newHash = $hasher->hash('images/photo.jpg');
echo $hash->distance($newHash);
```

### Parse from Base64

> public static Hash::fromBase64(string $base64): Hash

Create a Hash object from a Base64-encoded string. The method throws `InvalidArgumentException` if the Base64 string cannot be decoded.

#### Parameters

| Name | Type | Description |
| - | - | - |
| base64 | string | Base64-encoded hash value |

#### Example

```php
use Intervention\ImageHash\Hash;

// reconstruct from Base64 (e.g., from JSON API response)
$response = json_decode($apiResponse);
$hash = Hash::fromBase64($response->hash);

// use the reconstructed hash
$newHash = $hasher->hash('images/uploaded.jpg');
if ($hash->equals($newHash, leeway: 5)) {
    echo "Duplicate detected";
}
```

## Serialization

Hash objects implement `JsonSerializable` and `Stringable`, making them easy to use in various contexts.

### JSON Serialization

```php
use Intervention\ImageHash\Hash;

$hash = $hasher->hash('images/photo.jpg');

// automatically serializes to hex format
$json = json_encode($hash);
echo $json; // "8f9e9d8b0f0f1f07"

// works in arrays and objects
$data = [
    'image_id' => 123,
    'hash' => $hash,
    'timestamp' => time(),
];

echo json_encode($data);
// {"image_id":123,"hash":"8f9e9d8b0f0f1f07","timestamp":1234567890}
```

### String Casting

```php
use Intervention\ImageHash\Hash;

$hash = $hasher->hash('images/photo.jpg');

// cast to string (uses hex format)
echo (string) $hash; // "8f9e9d8b0f0f1f07"

// string interpolation
echo "Image hash: $hash"; // "Image hash: 8f9e9d8b0f0f1f07"

// concatenation
$filename = $hash . '.jpg';
```

### Debug Information

```php
use Intervention\ImageHash\Hash;

$hash = $hasher->hash('images/photo.jpg');

// var_dump shows useful debug info
var_dump($hash);
/*
object(Intervention\ImageHash\Hash)#1 (2) {
  ["hex"]=>
  string(16) "8f9e9d8b0f0f1f07"
  ["bitLength"]=>
  int(64)
}
*/
```
