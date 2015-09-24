### Application of BIP [32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), [38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki), [39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), [44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki), and 63 ([Stealth Addresses](http://sourceforge.net/p/bitcoin/mailman/message/31813471/)) to Altcoins

**Bitcoin-explorer's (bx)** command line interface (part of the libbitcoin tool suite) provides substantial BIP 32, 38, 39, and 63 support. BIP 44 capabilities for supporting altcoins results from how bx BIP 32 extended technology is applied, and the application of the table below. The "BIP44 Altcoin Version Mapping Table" below applies to BTC, and numerous other altcoins. This table also complements the [List of Address Prefixes](https://en.bitcoin.it/wiki/List_of_address_prefixes) top Table's "Hex" Column for row entries containing two hex digits.

The "BIP44 Altcoin Version Mapping Table" below is a work-in-progress, but an exemplar will provide important **"--version (-v)"** values for examples #1, #4, #5, and #6 below for an altcoin called Dash to demonstrate how BIPs 32, 38, 39 and 44 can be tightly integrated with minor extentions to coherently support altcoins. It is very important for wallet developers to understand these concepts to minimize complexity of wallets that are to support multiple currencies using a common hierarchical deterministic framework. The accuracy of portions of this table are not absolute (~90% > accuracy and strong trace-ability to implementation source code) until vetted by others, but the pattern for how it apply it  altcoins is firmly understood. This Table extends and complements [SLIP 44] (http://doc.satoshilabs.com/slips/slip-0044.html) referenced within [BIP44] (https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#registered-coin-types).  

#### BIP44 Altcoin Version Mapping Table
```
      |   BIP 44     |     mainnet     |     mainnet     |     mainnet    |   
Coin  | (coin_type’) |   version/WIF   |  version/p2pkh  |  version/p2sh  |   References
———————————————————————————————————————————————————————————————————————————————————————————————————————————————————
BTC   |       0      |       128       |         0       |        5       |   https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp
TEST  |       1      |       239       |       111       |      196       |   https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp
LTC   |       2      |       176       |        48       |        5       |   https://github.com/litecoin-project/litecoin/blob/master-0.10/src/chainparams.cpp
DOGE  |       3      |       158       |        30       |       22       |   https://github.com/dogecoin/dogecoin/blob/master/src/chainparams.cpp
RDD   |       4      |       189       |        61       |        5       |   https://github.com/reddcoin-project/reddcoin/blob/master/src/base58.h
DASH  |       5      |       204       |        76       |       16       |   https://github.com/dashpay/dash/blob/master/src/chainparams.cpp
PPC   |       6      |       183       |        55       |      117       |   https://github.com/super3/Peercoin.net -   see NBT base58.h
NMC   |       7      |       180       |        52       |       13       |   https://github.com/domob1812/namecore/blob/master/src/chainparams.cpp
FTC   |       8      |       142       |        14       |        5       |   https://github.com/FeatherCoin/Feathercoin/blob/master-0.8/src/base58.h
XCP   |       9      |       128       |       128?      |                |   Built on BTC, https://github.com/CounterpartyXCP/counterparty-lib  http://counterparty.io/docs/create_addresses/
BLK   |      10      |       153       |        25       |       25       |   https://github.com/rat4/blackcoin/blob/master/src/chainparams.cpp
NSR   |      11      |     149/191 c/u |        63       |       64       |   Built on PPC, https://nubits.com/nushares/introduction
NBT   |      12      |     150/191 c/u |        25       |       26       |   https://bitbucket.org/JordanLeePeershares/nubit/NuBit / src /base58.h, https://walletgenerator.net/?currency=Nubits
MZC   |      13      |       224       |        50       |        5       |   https://github.com/MazaCoin/MazaCoin/blob/master/src/base58.h, https://bitcointalk.org/index.php?topic=500312.0
VIA   |      14      |       199       |        71       |       33       |   https://github.com/viacoin/viacoin/blob/master/src/chainparams.cpp
XCH   |      15      |       199       |        71       |                |   Built on VIA, https://github.com/ClearingHouse/clearinghoused/blob/master/lib/config.py 
RBY   |      16      |       189       |        61       |       85       |   https://github.com/rubycoinorg/rubycoin/blob/master/src/base58.h
GRS   |      17      |       176       |        36?      |        5       | https://github.com/GroestlCoin/Groestlcoin-WPF/blob/master/coin-chains.xml (AddressVersion is 36)
DGC   |      18      |       153?      |        25?      |        5       | https://github.com/digibyte/digibyte/blob/master/src/chainparams.cpp
CCN   |      19      |       156       |        28       |        5       |   https://github.com/Cannacoin-Project/Cannacoin/blob/Proof-of-Stake/src/base58.h
DGB   |      20      |       128       |        30       |        5       |   https://github.com/digibyte/digibyte/blob/master/src/chainparams.cpp
OA?   |      21      |        23       |        19       |                |   https://github.com/OpenAssets/open-assets-protocol/blob/master/address-format.mediawiki#example ( % echo '00010966776006953d5567439e5e39f86a0d273bee' | bx base58check-encode -v 19  =>  Yields Open Assets Address: akB4NBW9UuCmHuepksob6yfZs6naHtRCPNy )
      |              |                 |                 |                |   https://github.com/OpenAssets/open-assets-protocol/blob/master/specification.mediawiki#protocol-overview ( % echo 'dup hash160 [ 010966776006953D5567439E5E39F86A0D273BEE ] equalverify checksig' | bx script-encode | bx sha256 | bx ripemd160  =>  Yields Open Assets ID: ALn3aK1fSuG27N96UGYB1kUYUpGKRhBuBC ; bx base58check-decode ALn3aK1fSuG27N96UGYB1kUYUpGKRhBuBC => Yields "version 23" )
XPM   |      24      |       151?      |        23       |                |  https://github.com/primecoin/primecoin/blob/master/src/base58.h
JBS   |      26      |       171?      |        43       |                |  https://github.com/jyap808/jumbucks/blob/master/src/base58.h
VTC   |      28      |       199?      |        71       |                |  https://github.com/vertcoin/vertcoin/blob/master/src/base58.h
NVC   |      50      |       136?      |         8       |                |  https://github.com/novacoin-project/novacoin/blob/master/src/base58.h
```

As a rule of thumb, any bx commands that support the "--version (-v)" values (an 8-bit number number in base10/decimal format) associated with private key functionality will use values from the **version/WIF** column for desired coin types. Any bx commands that support version values associated with single signature address functions for desired coin types will use the **version/p2pkh** column. Any bx commands that support version values associated with multisignature signature address functions for desired coin types will use the **version/p2sh** column. An empirical trend within the table above is that version/WIF values range between 128 and 255 inclusive. One notable exception discovered so far is for coin type 21, Open Assets that is a cryptocurrency agnostic token. Similarly, version/p2pkh values range between 0 and 127 inclusive. Not enough information has been gathered yet to pass judgement on the version/p2sh column value trends.

It is anticipated the libbitcoin approach presented here should be able to synthesize EC private keys and addresses for 100+ altcoins. Certainly there will be BIP/SLIP 44 registered coin types where it will not be readily apparent how to apply existing bx commands to arrive at associated WIF keys and/or addresses, e.g., coins with raw key lengths greater than 256 bits, or use hashing algorithms other that ripemd160, sha256, and sha512. Additionally, there will be altcoins that are not BIP/SLIP 44 registered that will have associated version/WIF and version/p2pkh values that will enable bx to easily create private EC keys and associated addresses. Such unregistered coin types will be included in the table above, but each having a blank "coin type".  If the libbitcoin framework is adopted by developers, it will naturally enable extended BIP 38 support for those altcoins. (Being investigated, but be patient... Single signature Stealth transaction creation services might also be able to be inherited if libbitcoin framework is applied.) 

Finally, to provide a foundation to jump start the establishment of numerous multi-coin wallet implementation, as a countermeasure to protect Bitcoin as goes through its pubescence growth phase, emphasis will first be applied towards populating the table above for coins that are BIP/SLIP 44 registered. It is anticipated once Bitcoin protocols(s) maturation/growth phase is completed, there will be a strong delineation between payment and settlement network processing layers that will implicitly support different levels of trust, with the settlement layer providing a greater amount of uncensored trust.

*It might be a bit much to digest at this point, but there are three additional columns technically required which are: testnet version/WIF, testnet version/p2pkh, and testnet version/p2sh. Albeit, having a testnet for a Testnet might seem redundant...*

### [bx - Wallet Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Wallet-Commands)

The table above is a "Rosetta Stone" that translates Bitcoin Elliptic Curve (EC) private keys and associated public addresses to those used by a number of altcoins having strong Bitcoin key/address synthesis heritage. This cryptocurrency Rosetta Stone currently provides important --version (-v) base10 integer values for the following **bitcoin-explorer** wallet command used to create addresses for numerous altcoins:

* **[ec-to-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-address)**  ( use version/p2pkh column for addresses )


**1) Combined BIP 32 and 44 Example:** *Apply M/44’/5’/0’/0/0 to create a compressed Dash public addresses for up to 4 billions addresses for safe use by an online machine!!!*

**A.** Be very afraid to use the weak brain wallet driven command sequence below on a computer that is online! Even with a very high entropy brain wallet, the approach below will will certainly be hacked unless you are a "cross domain solution" expert or apply multisignature technology as risk mitigators. However, this example is provided for explanation continuity purposes of 1B and 1C below.
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-public  -i 0 | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76
```
```   
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2
```

**B.** Is an equivalent M/44’/5’/0’/0 extended public key approach that protects the confidentiality of the master seed. Don't be afraid to apply the extended public key command sequence approach below to online computers. However, for privacy reasons, don't share extended keys beginning with xpub for Bitcoin or tpub for Testnet. (The prefix tpub below resulted from compiling bx with the "--enable-testnet" flag. Not compiling bx with this flag will results in a similar extended public key starting with xpub.)

```
% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76
```
```
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2
```
If crypto-currencies become more widely adopted, the approach above could severely diminish the need for eCommerce PCI-DSS compliance. This is a feature of permission-less blockchain technology! Permission-less blockchains don't require identity information to be utilized. This means permission-less cryptocurrency networks will naturally protect consumers from transaction payment identity theft for eCommerce transactions using a cryptocurrency transaction as payment/settlement. However, eCommerce servers accepting cryptographic currency payments utilizing such extended public keys must still protect the integrity of such extended public keys.  Otherwise, an eCommerce merchant risks customer payments being stolen or burned.
**C.** Demonstrates the generation of the next eCommerce Dash payment address (i.e., M/44’/5’/0’/0/1) to be applied by shopping cart checkout or point of sale (PoS) mechanisms, from the very same public extended key above (i.e., M/44’/5’/0’/0).
```
% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 1 | bx hd-to-ec | bx ec-to-address -v 76
```
```
XpTtgbcURSBfcuo8FZsNFeGrsCSi3jarAi
```


**2) BIP 39 Example:** *Create master seeds in Spanish from a common weak English brainwallet seed requiring the memorization of 15, 24 or 48 words.* Functionality demonstrated here is altcoin insensitive. The results below (i.e., 2B, 2D, 2F) makes a case that the more BIP 39 words, used from various spoken [languages](https://github.com/bitcoin/bips/blob/master/bip-0039/bip-0039-wordlists.md), used to create a deterministic BIP 32 master key don't necessarily mean greater security.

**A.**  Create seed for a 15 word representation for a BIP 39 encoded master seed.
```
% echo 'TREZOR' | bx base16-encode | bx ripemd160
```
```
0d7a259d0280785f98659ee9cb1809663cbd4672
```
**B.** 15 Spanish word BIP 39 representation of a master seed.
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx mnemonic-new -l es -p 0d7a259d0280785f98659ee9cb1809663cbd4672
```
```
anillo salón grosor afinar alacrán champú ganso pimienta todo fiel aceptar rojo rodar ombligo riñón
```

**C.** Create seed for a 24 word representation for a BIP 39 encoded master seed.
```
% echo 'TREZOR' | bx base16-encode | bx sha256
```
```
91d5a6684b637ded1e0d9eb7fea85a864ac3a7c44d666c3254b76108ae201550
```
**D.** 24 Spanish word BIP 39 representation of a master seed.
```
echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx mnemonic-new -l es -p 91d5a6684b637ded1e0d9eb7fea85a864ac3a7c44d666c3254b76108ae201550
```
```
moler pausa nevar música conocer veinte júpiter pimienta pollo valor átomo ancho pasar seco arbusto pata hígado monto célebre raspa matriz aprender familia apoyo
```

**E.** Create seed for a 48 word representation for a BIP 39 encoded master seed.
```
echo 'TREZOR' | bx base16-encode | bx sha512
```
```
4da2ce0586c67550f627d108d4b0352646add71253a1d647076f9ffa3b6d1379c6f6f4c8e49a185344ee272d1a66a185329686a42ef61bf08782d595fc313824
```
**F.** 48 Spanish word BIP 39 representation of a master seed.
```
echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx mnemonic-new -l es -p 4da2ce0586c67550f627d108d4b0352646add71253a1d647076f9ffa3b6d1379c6f6f4c8e49a185344ee272d1a66a185329686a42ef61bf08782d595fc313824
```
```
enredo ático litro ánimo grosor paella símbolo viejo aleta orgía ángulo encía hebra torpedo edificio invierno sermón copa sostén dedo opción pluma enseñar cordón velero orquesta coser clínica luz olfato pompa terror babor codo gancho gordo guía evitar proeza rechazo tubo cuchara pizca carta rebote nota mirar curioso
```


**3) BIP 39 Example:** *Recreate a master seed from BIP 39 words.* Functionality demonstrated here is altcoin insensitive.
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


### [bx - Encoding Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Encoding-Commands)

Most encoding commands supporting **--version** are not restricted as to which of the two columns to use since these commands can be used to develop either WIF private keys, or associated coin addresses. The following bitcoin explorer "encoding commands" provide version support:

* **[address-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-address-encode)** ( use version/p2pkh column for addresses )
* **[base58check-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-base58check-encode)** ( use version/WIF column for private keys, or version/p2pkh column for addresses )
* **[wrap-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-wrap-encode)** ( use version/WIF column for private keys**, or version/p2pkh column for addresses )


**4) Combined BIP 32 and 44 Example:** *Apply m/44’/5’/0’/0/0 example to create a compressed Dash private key.*

**A.** Synthesized compressed EC private key below is derived from a very weak cryptographical brain wallet. Note that this affords absolutely no protection of the master seed that feeds the hd-new.  The piped "sed 's/$/01/'" command below appends the private key with "01" which signals the key is compressed. Without this extra suffix, the EC public key is in the uncompressed form. 
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204 
```
```                                                                    
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM
```

**B.** This m/44’/5’/0’/0 extended private key synthesis approach, derived from the same cryptographically weak brain wallet, also protects the confidentiality of the master seed.  However, extreme care must still be exercised to protect the confidentiality of extended private keys starting with xprv or tprv. A compromise of the confidentiality of m/44’/5’/0’/0 for this Dash example will likely compromise the funds for up ~4 billion synthesized addresses. (The prefix tprv below resulted below from compiling bx with the "--enable-testnet" flag. Not compiling bx with with this flag results in a similar extended private key starting with xprv.)
```
% echo  'tprv8iBUTxFHtPMKmrQDN4yjCPWmNBT9ZPZZeSFgxNLnAhmNmsHVmFxENnREcdEQXLVUoE3invSjhTjDsHfCrVtijVvVYbj6XWfH6DmQnXQvQoZ' | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204
```
```
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM
```

**C.** Uses the same m/44’/5’/0’/0 extended private key that protects the confidentiality of the master seed to create m/44’/5’/0’/0/1.
```
% echo 'tprv8iBUTxFHtPMKmrQDN4yjCPWmNBT9ZPZZeSFgxNLnAhmNmsHVmFxENnREcdEQXLVUoE3invSjhTjDsHfCrVtijVvVYbj6XWfH6DmQnXQvQoZ' | bx hd-private -i 1 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204
```
```
XGobHujzvnXWdnteE2aZU8TH2EEgbWkXr9iFQuU9QL1mpU21brja
```

### [bx - Key Encryption Commands] (https://github.com/libbitcoin/libbitcoin-explorer/wiki/Key-Encryption-Commands)

The table above also complements [Altchain Encrypted Private Keys](https://github.com/libbitcoin/libbitcoin/wiki/Altchain-Encrypted-Private-Keys#sample-map) by supporting the following **bitcoin-explorer** "encrypted key" commands to extend **alpha BIP 38 functionality** to altcoins:

* **[ec-to-ek](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-ek)** ( use version/WIF column for private keys )
* **[ek-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-address)**  ( use version/p2pkh column for addresses )
* **[ek-new](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-new)** ( use version/WIF column for private keys )
* **[ek-public](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-public)**  ( use version/p2pkh column for addresses )


**5) Extended AES256Encrypt and AES256Decrypt BIP 38 Example:** *For a Dash base16-encoded 256-bit secret elliptic curve key.*

**A.** Extended BIP 38 (256 bit AES) encryption for Dash of a base16 encoded EC private key.
```
% bx ec-to-ek -v 204 'Hello it is me' f9a8f6d4a24b99d4944ee3db83c85383e9c13e85cb50ad60a9e1a96e02f6d269
```
```
5XCsGSbMhW6zisvPx7LUKHPUGTi21kdSVwc6HNM1Zurg9ENPiUVtzBZDho
```
**B.** Extended BIP 38 (256 bit AES) decryption of an extended Dash BIP 38 encrypted base16 encoded EC private key.
```
% bx ek-to-ec 'Hello it is me' 5XCsGSbMhW6zisvPx7LUKHPUGTi21kdSVwc6HNM1Zurg9ENPiUVtzBZDho
```
```
f9a8f6d4a24b99d4944ee3db83c85383e9c13e85cb50ad60a9e1a96e02f6d269
```


**6) Extended "EC Multiply Mode" BIP 38 Example:** *For Dash having an initial secret of 'knock knock', seed, salt, lot number of 0, and sequence number of 0. (Please note the information below needs to be correlated with security [recommendations](https://github.com/libbitcoin/libbitcoin/wiki/BIP38-Security-Considerations#recommendations) to arrive at a good processes for outsourcing the minting of coins or engraving of notes by the owners of Dash funds.)*

**A.** "Brain seed"
```
% echo 'Not so random seed' | bx base16-encode | bx sha256
```
```
565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```

**B.** "Brain salt" utilizes the first 8 hex digits below.
```
% echo 'a little salt & pepper' | bx base16-encode | bx sha256
```
```
e51549349dd7b98ff30281211fe281247c32922d259fc12b0abf7b2110114d03
```

**C.**  Is typically performed only by a coin/note owner prior committing to outsourcing work to a minter/engraver. Both this information and the associated seed are released only to the minter/engraver. Intermediate codes are always prefixed with "passphrase".
```
% bx token-new -l 0 -s 0 'knock knock' e5154934
```
```
passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg
``` 

**D.** Is performed by the minter/engraver to know the BIP 38 encrypted private key to be publicly labelled on a Dash coin/note.
```
% bx ek-new -v 204 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```
```
5XTqTrYMNKoHHcfqafEX5nFZTLnNwXF5Zf6fjYP8cDqNDwzPxendxaCMGw
``` 

**CP1.** Computed EC Dash private key - comparison point #1
```
% bx ek-to-ec 'knock knock' 5XTqTrYMNKoHHcfqafEX5nFZTLnNwXF5Zf6fjYP8cDqNDwzPxendxaCMGw
```
```
cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23
```

**CP2.** Traditional computation of an EC Dash public key - comparison point #2
```
% echo 'cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23' | bx ec-to-public
```
```
035d37339d296b1a7ea8c7f04cf33eb0e8fd547df58d60259c9e4d9404795cd7f1
```

**CP3.** Traditional computation of the associated Dash address - comparison point #3
```
% echo 'cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23' | bx ec-to-public  | bx ec-to-address -v 76
```
```
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu
``` 

**E.** To be created by a minter/engraver. To avoid being classified as "money transmitter", minter/engraver must not send/share this information with the coin/note owner until after the coin/note is sent by registered mail, preferably delivered. However, there are no explicit counter measures to prevent entrapment by a "devious" coin/note owner that is built into the BIP 38 "multiply mode" capability!!!
```
% bx ek-public -v 76 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```
```
cfrm3CdFNyDReVUXn2weQYL4Q3sGsRyFYSNBbrK5qfpFyCXCNKPPJicRxuxmLiN3ZtjVafCLZuc
```

**V1.** Validation #1 - Matches CP2
```
% bx ek-public-to-ec 'knock knock' cfrm3CdFNyDReVUXn2weQYL4Q3sGsRyFYSNBbrK5qfpFyCXCNKPPJicRxuxmLiN3ZtjVafCLZuc
```
``` 
035d37339d296b1a7ea8c7f04cf33eb0e8fd547df58d60259c9e4d9404795cd7f1
```

**F.** Is performed by a coin/note owner after receiving the confirmation code from their minter/engraver.  If public address doesn't match the results of the next command, coin/note owner should not "load" the coin with the denomination printed on the coin. Observe the result matches CP3.
```
% bx ek-public-to-address 'knock knock' cfrm3CdFNyDReVUXn2weQYL4Q3sGsRyFYSNBbrK5qfpFyCXCNKPPJicRxuxmLiN3ZtjVafCLZuc
```
```
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu
```

**G.** Is performed by a coin/note owner to double authenticate the Dash coin address where funds are to be deposited. There could be a typo mistake, cut-and-paste mistake, or a man-in-the-middle attack (e.g., from utilizing an untrusted communication channel between the minter/engraver and coin/note owner)  compromising the integrity of the confirmation code resulting in a bad address created by step 6F. If results match, a deposit is not likely to be lost or burned. Observe the result below matches CP3
```
% bx ek-address -v 76 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```
```
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu
```


### [bx - Stealth Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Stealth-Commands)

The application **--version** values to **Stealth Commands** for altcoins is a work in progress...

The following bitcoin explorer wallet stealth commands are natural candidates to be extended to accommodate **--version** values:

* **[stealth-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-stealth-encode)** ( recommend using version/p2pkh column )
* *other stealth commands are under investigation*


### [bx - Transaction Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Transaction-Commands)

* **[script-to-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-script-to-address)** (recommend using version/p2sh column)
