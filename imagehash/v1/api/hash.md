---
label: "Hash Object"
title: "Working with Hash Objects"
subtitle: "Compare, Convert and Store Image Hashes"
lead: "Work with Hash objects to compare and detect similar images. Convert between formats and reconstruct hashes from stored values in PHP."
sort: 2
---

[TOC]

When you generate an image hash using any hashing strategy, you get a `Hash` object that implements `HashInterface`. This object represents a perceptual fingerprint of the image. It's **immutable**, **serializable**, and **comparable**.

## Comparing Hashes

Perceptual hashes can be compared to determine image similarity. The library uses the Hamming distance algorithm, which counts the number of differing bits between two hashes.

### Calculate Distance

> public Hash::distance(HashInterface $hash): int

Calculate the Hamming distance between two hashes. This returns the number of bits that differ. Lower distance means more similar images.

#### Parameters

| Name | Type | Description |
| - | - | - |
| hash | HashInterface | The hash to compare against |

#### Return Value

Returns an integer representing the number of differing bits. A distance of `0` means the hashes are identical.

Both hashes must have the same bit length. If the GMP extension is available, the method uses `gmp_hamdist()` for faster comparison. Otherwise, it falls back to array comparison (still fast, just slightly slower).


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

Check if two hashes are equal within an optional tolerance. This is a convenience wrapper around the distance method.

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

Hash objects support multiple output formats for storage, transmission, or display. All conversions are lossless and reversible.

### Convert to Hexadecimal

> public Hash::toHex(): string

Convert the hash to hexadecimal. This is the most common storage format and the default string representation.

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

Convert the hash to binary string format (concatenated "0" and "1" characters).

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

Get the raw byte string. This is how the hash is stored internally.

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

Convert to Base64 encoding. Useful for JSON, URLs, or text-based protocols.

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

Get the total number of bits in the hash. Different strategies and settings produce different bit lengths.

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

You can reconstruct a `Hash` object from previously stored values using static factory methods. This is useful for comparing new hashes against stored ones.

### Parse from Hexadecimal

> public static Hash::fromHex(string $hex): Hash

Create a Hash from hexadecimal. The method validates input and throws `InvalidArgumentException` if parsing fails.

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

Create a Hash from binary string or array of bit values. Accepts multiple formats:

- String of "0" and "1" characters: `"10011010"`
- Array of integers: `[1, 0, 0, 1, 1, 0, 1, 0]`
- Array of booleans: `[true, false, false, true]`
- Array of strings: `["1", "0", "0", "1"]`

The method validates input and throws `InvalidArgumentException` if the bits cannot be converted to an image hash.

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

Create a Hash from raw bytes.

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

Create a Hash from Base64. Throws `InvalidArgumentException` if decoding fails.

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
