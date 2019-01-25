---
description: This describes the low level minutia for common data structures.
---

# Building blocks

## Chain Name

A Chain Name is a value to uniquely identify a Chain. It can be a random number, a string of text, a public key, or hash of some private directory path. The choice of Chain Name is left up to the user. The Chain Name can be specified with multiple sequential byte strings. They are treated as different segments of data instead of concatenated, to differentiate trailing bytes of one segment from leading bytes of the next segment.

The individual segment length are limited by how many bytes can fit in an Entry \(approx 10 KiB\). Each Chain Name element must be at least 1 byte long. A Chain Name with no elements is a special case where the ChainID is the hash of a null string:`e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`.

## ChainID

A ChainID is a series of SHA256 hashes of Chain Name segments. The ChainID is 32 bytes long. The ChainID must be the hash of _something_ to only have opaque data in the higher level block structures.

The algorithm hashes each segment of the Chain Name. Those hashes are concatenated, and are hashed again into a single 32 byte value.

Getting a ChainID from a single segment Chain Name would be equivalent of hashing the Chain Name twice.

$$
ChainID = SHA256( SHA256(Name[0]) | SHA256(Name[1]) | ... | SHA256(Name[X]) )
$$

## 

