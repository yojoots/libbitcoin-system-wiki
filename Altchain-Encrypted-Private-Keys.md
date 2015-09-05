We consider it important that libbitcoin support Bitcoin features to the extent that they are envisioned by supported proposals. For example, the [payment address version](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-address#example-4). There is no limit to the diversity of features that may deviate from this in altcoins, so its not possible for us to support all altcoins generally. We draw the line at support for *altchains*. To the extent that an *altcoin* appears like Bitcoin but with a different genesis block, we should support it.

> Support beyond this criteria is not on the radar, with one exception. We will eventually support pluggable consensus checks, given that altchains are defined by distinct consensus rules. It is our goal to support altchains without a rebuild of any library. So any libbitcoin binary supports them all (with a requirement for additive consensus plugins).

These considerations drive the outcome on this question. There are three [base58check](https://en.bitcoin.it/wiki/Base58Check_encoding) (serializable) primitives associated with [BIP-38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki), which libbitcoin refers to as follows:

* `private_key` : encrypted private key 
* `public_key` : encrypted public key
* `intermediate` : intermediate passphrase string

In accordance with BIP-38 these have the following prefix values:
```cpp
namespace prefix
{
    // This prefix results in the prefix "6P" in the base58 encoding.
    static const data_chunk private_key
    {
        0x01, 0x42
    };

    // This prefix results in the prefix "6P" in the base58 encoding.
    static const data_chunk private_key_multiplied
    {
        0x01, 0x43
    };

    // This prefix results in the prefix "cfrm" in the base58 encoding.
    static const data_chunk public_key
    {
        0x64, 0x3b, 0xf6, 0xa8, 0x9a
    };

    // This prefix results in the prefix "passphrase" in the base58 encoding.
    static const data_chunk lot_intermediate
    {
        0x2c, 0xe9, 0xb3, 0xe1, 0xff, 0x39, 0xe2, 0x51
    };

    // This prefix results in the prefix "passphrase" in the base58 encoding.
    static const data_chunk intermediate
    {
        0x2c, 0xe9, 0xb3, 0xe1, 0xff, 0x39, 0xe2, 0x53
    };
}
```
The first byte of each of these is the [base58check version](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-base58check-encode#example-2). This of course should not be confused with a payment address base58check version. BIP-38 serializes payment addresses before hashing. So there is also a payment address version affecting each of the three primitives. Notably the [compression option for ec public keys](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-address#example-1) also affects these artifacts.

BIP-38 carries the compression flag through the encoding. As a consequence there is no need to have knowledge of the compression value used in creation of the keys in order to decrypt the keys. This is not the case with the payment address version. One of three scenarios exist that are consistent with BIP-38:

1. The payment address version is always Bitcoin mainnet `0x01` (with compression specified at encryption time).
2. The payment address version and compression are specified at encryption time, and the correct payment address version *must also* be provided at decryption time.
3. The payment address version and compression are specified only at encryption time.

The first doesn’t even support testnet. The second is poor from a user scenario perspective. The third provides support for altchains that is consistent with BIP38 behavior for Bitcoin mainnet. There are two ways to implement this option:

 1. Hard code a mapping between [well-known payment address versions](https://en.bitcoin.it/wiki/List_of_address_prefixes) and corresponding encrypted key versions.
 2. Define a deterministic mapping from the payment address to the encrypted private key address.

### Proposal

Given that encrypted keys already have a dependency on payment address versions there appears to be no reason to support a non-deterministic version mapping. A deterministic mapping is straightforward and future-proofed against ongoing changes to declared address versions and encrypted key prefixes.

### Backward Compatibility

A deterministic mapping is straightforward. The payment address version can simply be coupled to the base58check version byte for a corresponding encrypted private key. There is however one idiosyncrasy required for backward compatibility.

BIP-38 proposes `0x01` as the base58check version byte for `private_key`. Based on test vectors this corresponds to the Bitcoin mainnet payment address version of `0x00`. As such the following bidirectional mapping is proposed.

```cpp
static inline uint8_t convert_version(const uint8_t version)
{
    switch (version)
    {
        case 0:
            return 1;
        case 1:
            return 0;
        default:
            return version;
    }
}
```

### Cosmetic Inflexibility

A possible problem would be inflexibility in the cosmetics of the first couple of characters in encrypted private keys. Some choice would remain with a deterministic mapping, but it would be coupled to the choice of payment address version and would be limited to one byte. In other words each could not be independently chosen for the same altchain.

### Limited Payment Address Version Domain

It is also true that there is a finite domain of 256 values for the payment address version. However this issue cannot be resolved by expanding the domain of encrypted private keys that are coupled to that domain. It seems preferable to attach any change to the encrypted key domain to a corresponding expansion of the payment address domain.

### Effect on Serialized Artifacts
The implementation as described has no impact on `intermediate` or `private_key` artifacts. These retain the cosmetic prefixes described by BIP-38:

* `public_key` : "cfrm"
* `intermediate` : "passphrase"

As such these values will become chain ambiguous. However had the intent been to associate these values by chain it seems unlikely that these natural language prefixes would have been chosen, as they have no self-evident correlation to the cryptic `6P` value. Any deterministic deviation would require abandoning these natural language cosmetics. Additionally the scenario objectives are satisfied without mutating the cosmetics of these serializations.