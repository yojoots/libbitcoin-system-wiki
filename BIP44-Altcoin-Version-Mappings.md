### Application of BIP [32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), [38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki), [39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), [44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki), and 63 ([Stealth Addresses](http://sourceforge.net/p/bitcoin/mailman/message/31813471/)) to Altcoins

**Bitcoin-explorer's (bx)** command line interface (part of the libbitcoin tool suite) provides substantial BIP 32, 38, 39, and 63 support. BIP 44 capabilities results from how bx BIP 32 is applied, and the application of the table below. The "BIP44 Altcoin Version Mapping Table" below applies to BTC and numerous other altcoins. This table also complements the [List of Address Prefixes](https://en.bitcoin.it/wiki/List_of_address_prefixes) top Table's Hex Column with row entries containing two hex digits.

This "BIP44 Altcoin Version Mapping Table" is a work-in-progress, but provides important values for examples #1 and #4 below the table. Accuracy of portions of this table is questionable (~90% accurate) until vetted by others, but the pattern for how it is applies to altcoins is well understood. This Altcoin Version Mapping Table most definitely extends/complements [SLIP 44] (http://doc.satoshilabs.com/slips/slip-0044.html) referenced within [BIP44] (https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#registered-coin-types)

#### BIP44 Altcoin Version Mapping Table
```
      |              |                    |                 |
Coin  |   BIP 44     |    version/WIF     |  version/p2pkh  |   References
      | (coin_type’) |                    |                 |
———————————————————————————————————————————————————————————————————————————————————————————————————————————————————
BTC   |       0      |        128         |         0       |   https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp
TEST  |       1      |        239         |       111       |   https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp
LTC   |       2      |        176         |        48       |   https://github.com/litecoin-project/litecoin/blob/master-0.10/src/chainparams.cpp
DOGE  |       3      |        158         |        30       |   https://github.com/dogecoin/dogecoin/blob/master/src/chainparams.cpp
RDD   |       4      |        189         |        61       |   https://github.com/reddcoin-project/reddcoin/blob/master/src/base58.h
DASH  |       5      |        204         |        76       |   https://github.com/dashpay/dash/blob/master/src/chainparams.cpp
PPC   |       6      |        183         |        55       |   https://github.com/super3/Peercoin.net -   see NBT base58.h
NMC   |       7      |        180         |        52       |   https://github.com/domob1812/namecore/blob/master/src/chainparams.cpp
FTC   |       8      |        142         |        14       |   https://github.com/FeatherCoin/Feathercoin/blob/master-0.8/src/base58.h
XCP   |       9      |        128         |       128?      |   Built on BTC, https://github.com/CounterpartyXCP/counterparty-lib  http://counterparty.io/docs/create_addresses/
BLK   |      10      |        153         |        25       |   https://github.com/rat4/blackcoin/blob/master/src/chainparams.cpp
NSR   |      11      |        149/191 c/u |        63       |   Built on PPC, https://nubits.com/nushares/introduction
NBT   |      12      |        150/191 c/u |        25       |   https://bitbucket.org/JordanLeePeershares/nubit/NuBit / src /base58.h, https://walletgenerator.net/?currency=Nubits
MZC   |      13      |        224         |        50       |   https://github.com/MazaCoin/MazaCoin/blob/master/src/base58.h, https://bitcointalk.org/index.php?topic=500312.0
VIA   |      14      |        199         |        71       |   https://github.com/viacoin/viacoin/blob/master/src/chainparams.cpp
XCH   |      15      |        199         |        71       |   Built on VIA, https://github.com/ClearingHouse/clearinghoused/blob/master/lib/config.py 
RBY   |      16      |        189         |        61       |   https://github.com/rubycoinorg/rubycoin/blob/master/src/base58.h
GRS   |      17      |        176         |        36?      | https://github.com/GroestlCoin/Groestlcoin-WPF/blob/master/coin-chains.xml (AddressVersion is 36)
DGC   |      18      |        153?        |        25?      | https://github.com/digibyte/digibyte/blob/master/src/chainparams.cpp
CCN   |      19      |        156         |        28       |   https://github.com/Cannacoin-Project/Cannacoin/blob/Proof-of-Stake/src/base58.h
DGB   |      20      |        128         |        30       |   https://github.com/digibyte/digibyte/blob/master/src/chainparams.cpp
OA?   |      21      |         23         |        19       |   https://github.com/OpenAssets/open-assets-protocol/blob/master/address-format.mediawiki#example ( % echo '00010966776006953d5567439e5e39f86a0d273bee' | bx base58check-encode -v 19  =>  Yields Open Assets Address: akB4NBW9UuCmHuepksob6yfZs6naHtRCPNy )
      |              |                    |                 |   https://github.com/OpenAssets/open-assets-protocol/blob/master/specification.mediawiki#protocol-overview ( % echo 'dup hash160 [ 010966776006953D5567439E5E39F86A0D273BEE ] equalverify checksig' | bx script-encode | bx sha256 | bx ripemd160  =>  Yields Open Assets ID: ALn3aK1fSuG27N96UGYB1kUYUpGKRhBuBC ; bx base58check-decode ALn3aK1fSuG27N96UGYB1kUYUpGKRhBuBC => Yields "version 23" )
XPM   |      24      |        151?        |        23        |  https://github.com/primecoin/primecoin/blob/master/src/base58.h
JBS   |      26      |        171?        |        43        |  https://github.com/jyap808/jumbucks/blob/master/src/base58.h
VTC   |      28      |        199?        |        71        |  https://github.com/vertcoin/vertcoin/blob/master/src/base58.h
NVC   |      50      |        136?        |         8        |  https://github.com/novacoin-project/novacoin/blob/master/src/base58.h
```

As a rule of thumb, any bx commands that support the **--version (-v)** values (an 8 bit decimal number) associated with private keys will use values from the **version/WIF** column for a desired coin. Similarly, any bx commands that support version values associated with coin addresses for a desired coin will use the **version/p2pkh** column. An empirical trend within the table below is that version/WIF values range between 128 and 255 inclusive. Similarly, version/p2pkh values range between 0 and 127 inclusive. 

*There will be altcoins that are not BIP/SLIP 44 registered that will have associated version/WIF and version/p2pkh values that will enable bx to synthesize private EC keys and associated addresses. Such a table will be created at a later date.  However, emphasis will be applied toward coins that are BIP/SLIP 44 registered to help boost the establishment of multi-coin wallets.*

### [Wallet Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Wallet-Commands)

The table above is a "Rosetta Stone" to effectively translate Bitcoin private keys and public addresses to those used by a number of altcoins having strong Bitcoin heritage. It provides important --version (-v) base10 integer values for the following **bitcoin-explorer** commands to be used to addresses for altcoins:

* **[ec-to-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-address)**  ( use version/p2pkh column for addresses )


**1) Combined BIP 32 and 44 Example:** Apply m/44’/5’/0’/0/0 to create a compressed Dash public addresses for up to 4 billions addresses much more safely on an online machine!!!

A. *Be very afraid to use this weak brain wallet driven command sequence below on an online computer!*
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-public  -i 0 | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76
```
```   
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2
```
B. *Don't be afraid to apply the chain code driven command sequence below on an online computer. However, for privacy reasons, don't share keys beginning with xpub for Bitcoin or tpub for Testnet. (If crypto-currencies become more widely adopted, this approach could be a death knell to eCommerce PCI-DSS compliance.)*
```
% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76
```
```
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2
```
C. *Demonstrates the generation of the next public key, i.e., m/44’/5’/0’/0/1, from the same public key chain code above.*
```
% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 1 | bx hd-to-ec | bx ec-to-address -v 76
```
```
XpTtgbcURSBfcuo8FZsNFeGrsCSi3jarAi
```

**2) BIP 39 Example:** Create master seed in Spanish from a weak English brainwallet seed. (Is altcoin insensitive.)
```
% echo 'very complex gibberish' | bx base16-encode | bx sha512 | bx mnemonic-new -l es
```
```
cambio cosmos leche dar imponer enfermo envío equipo tanque liso utopía semilla altar bebé proa caoba maestro bodega equipo escribir droga paso apodo bulto vela molino nave talento militar perder odiar árido signo enfermo rojizo ganso himno clase átomo chupar rienda quitar ciclón banda situar rueda alto asesor
```

**3) BIP 39 Example:** Recreate master seed from BIP 39 words. (Is altcoin insensitive.)
```
% echo 'enable load garage hard diagram trim nothing exclude fantasy gold ramp fiber wise ball have hero toddler spy excite glue maze drill else sell' | bx mnemonic-to-seed -p TREZOR
```
```
f0e63d191d75d39b5d1d8d1ae8ff1c48e51cacffb6d3881f31715572a59f352d35fa44a7e84f9a69712b206b9e04966a5794470993516e1b363a001fc3917f69
```

The following bitcoin explorer wallet commands are natural candidates to be extended to accommodate **--version** values:

* **[ec-to-wif](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-wif)**          ( recommend using version/WIF column for private keys )
* **[hd-to-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-hd-to-address)**      ( recommend using version/p2pkh column for addresses )
* **[hd-to-wif](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-hd-to-wif)**          ( recommend using version/WIF column for private keys )


### [Encoding Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Encoding-Commands)

Some encoding commands supporting **--version** are not restricted as to which of the two columns to use since these commands can be used to develop either WIF private keys, or associated coin addresses. The following bitcoin explorer "encoding commands" provide version support:

* **[address-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-address-encode)** ( use version/p2pkh column for addresses )
* **[base58check-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-base58check-encode)** ( use version/WIF column for private keys, or version/p2pkh column for addresses )
* **[wrap-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-wrap-encode)** ( use version/WIF column for private keys**, or version/p2pkh column for addresses )

**4) Combined BIP 32 and 44 Example:** Apply m/44’/5’/0’/0/0 example to create a compressed Dash private key.

A. *Synthesized EC private key below is derived from a very weak cryptographical brain wallet* 
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204 
```
```                                                                    
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM
```

B. *Equivalent chain code-driven EC private key synthesis, derived from a cryptographically weak brain wallet.  Extreme care must be exercised to protect the confidentiality of chain code starting with xprv or tprv.*
```
% echo 'tprv8iBUTxFHtPMKmrQDN4yjCPWmNBT9ZPZZeSFgxNLnAhmNmsHVmFxENnREcdEQXLVUoE3invSjhTjDsHfCrVtijVvVYbj6XWfH6DmQnXQvQoZ' | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204
```
```
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM
```

### [Key Encryption Commands] (https://github.com/libbitcoin/libbitcoin-explorer/wiki/Key-Encryption-Commands)

The table above also complements [Altchain Encrypted Private Keys](https://github.com/libbitcoin/libbitcoin/wiki/Altchain-Encrypted-Private-Keys#sample-map) by supporting the following **bitcoin-explorer** "encrypted key" commands to extend **alpha BIP 38 functionality** to altcoins:

* **[ec-to-ek](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-ek)** ( use version/WIF column for private keys )
* **[ek-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-address)**  ( use version/p2pkh column for addresses )
* **[ek-new](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-new)** ( use version/WIF column for private keys )
* **[ek-public](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-public)**  ( use version/p2pkh column for addresses )

**5) Extended AES256Encrypt and AES256Decrypt BIP 38 Example:** For a Dash base16-encoded 256-bit secret elliptic curve key.

A. *Extended BIP 38 (256 bit AES) encryption of a Dash coin private key.*
```
% bx ec-to-ek -v 204 'Hello it is me' f9a8f6d4a24b99d4944ee3db83c85383e9c13e85cb50ad60a9e1a96e02f6d269
```
```
5XCsGSbMhW6zisvPx7LUKHPUGTi21kdSVwc6HNM1Zurg9ENPiUVtzBZDho
```
B. *Extended BIP 38 (256 bit AES) decryption of an extended BIP 38 encrypted Dash coin private key.*
```
% bx ek-to-ec 'Hello it is me' 5XCsGSbMhW6zisvPx7LUKHPUGTi21kdSVwc6HNM1Zurg9ENPiUVtzBZDho
```
```
f9a8f6d4a24b99d4944ee3db83c85383e9c13e85cb50ad60a9e1a96e02f6d269
```

**6) Extended "EC Multiply Mode" BIP 38 Example:** For Dash with an initial secret of 'knock knock', seed, salt, lot number of 0, and sequence number of 0. *Please note the information below must be correlated with security [recommendations](https://github.com/libbitcoin/libbitcoin/wiki/BIP38-Security-Considerations#recommendations) to arrive at a good processes for minting coins or engraving notes.*

A. *A "brain seed".*
```
% echo 'Not so random seed' | bx base16-encode | bx sha256
```
```
565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```

B. *"Brain salt" utilizes the first 8 hex digits below.*
```
% echo 'a little salt & pepper' | bx base16-encode | bx sha256
```
```
e51549349dd7b98ff30281211fe281247c32922d259fc12b0abf7b2110114d03
```

C. *Intermediate code (passphrase*) created by the future coin/note owner to outsource work to a minter/engraver. Both this information and the seed are released only to the minter/engraver.*
```
% bx token-new -l 0 -s 0 'knock knock' e5154934
```
```
passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg
``` 

D. *Performed by the minter/engraver to know the BIP 38 encrypted private key to be publicly labelled on a Dash coin/note.*
```
% bx ek-new -v 204 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```
```
5XTqTrYMNKoHHcfqafEX5nFZTLnNwXF5Zf6fjYP8cDqNDwzPxendxaCMGw
``` 

TP1. *Computed EC Dash private key - test point #1*
```
% bx ek-to-ec 'knock knock' 5XTqTrYMNKoHHcfqafEX5nFZTLnNwXF5Zf6fjYP8cDqNDwzPxendxaCMGw
```
```
cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23
```

TP2. *Traditional computation of an EC Dash public key - test point #2*
```
% echo 'cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23' | bx ec-to-public
```
```
035d37339d296b1a7ea8c7f04cf33eb0e8fd547df58d60259c9e4d9404795cd7f1
```

TP3. *Traditional computation of the associated Dash address - test point #3*
```
% echo 'cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23' | bx ec-to-public  | bx ec-to-address -v 76
```
```
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu
``` 

E. *Created by the minter/engraver. To avoid being classified as "money transmitter", minter/engraver must not send/share this information with the coin/note owner until after the coin/note is sent by registered mail, preferably delivered. However, there are no explicit counter measures preventing entrapment by a "devious" coin/note owner by the BIP 38 protocol!!!*
```
% bx ek-public -v 76 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```
```
cfrm3CdFNyDReVUXn2weQYL4Q3sGsRyFYSNBbrK5qfpFyCXCNKPPJicRxuxmLiN3ZtjVafCLZuc
```

V1. *Validation #1 - Matches TP2*
```
% bx ek-public-to-ec 'knock knock' cfrm3CdFNyDReVUXn2weQYL4Q3sGsRyFYSNBbrK5qfpFyCXCNKPPJicRxuxmLiN3ZtjVafCLZuc
```
``` 
035d37339d296b1a7ea8c7f04cf33eb0e8fd547df58d60259c9e4d9404795cd7f1
```

F. *Performed by coin/note owner after receiving the confirmation code from the minter/engraver.  If public address doesn't match the results of the next command, coin/note owner should not "load" the coin with the denomination printed on the coin. Observe the result matches TP3*
```
% bx ek-public-to-address 'knock knock' cfrm3CdFNyDReVUXn2weQYL4Q3sGsRyFYSNBbrK5qfpFyCXCNKPPJicRxuxmLiN3ZtjVafCLZuc
```
```
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu
```

G. *Performed by coin/note owner to authenticate the Dash coin address where funds are to be deposited. If there is a match, a deposit is not likely to be lost or burned. Observe the result matches TP3*
```
% bx ek-address -v 76 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```
```
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu
```


### [Stealth Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Stealth-Commands)

The application **--version** values to **Stealth Commands** for altcoins is a work in progress...

The following bitcoin explorer wallet stealth commands are natural candidates to be extended to accommodate **--version** values:

* **[stealth-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-stealth-encode)**      ( recommend using p2pkh column )
* *more commands are under investigation*

