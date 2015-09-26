### Application of BIP [32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), [38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki), [39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), [44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki), and 63 ([Stealth Addresses](http://sourceforge.net/p/bitcoin/mailman/message/31813471/)) to Altcoins

**Bitcoin-explorer's (bx)** command line interface (CLI), part of the libbitcoin tool suite, provides very substantial support for the following Bitcoin Improvement Proposals (BIP): 32, 38, 39, and 63.  BIP 44 capabilities for supporting alternative cryptocurrency coins (altcoins) results from how bx will openly extend these BIPs in an integrated manner, and the application of the table below. Behaviors associated with using column version values from the first row of the "BIP44 Altcoin Version Mapping Table" below are natively integrated into bitcoin-explorer's commands defaults. 

The libbitcoin team understands the intricacies of these defaults table values when applied to Bitcoin (BTC), and is in the midst of updating a small subset of existing bx command line interfaces with only the addition of one argument (already supported by a few select commands) that will enable support for 100+ other altcoins. This could potentially create a common code base, a merge, fostering convergence of existing Bitcoin code forks, but those decisions are left to altcoin main branch developers.

The table below is a work-in-progress, but as an exemplar, it provides important **"--version (-v)"** values for examples #1, #4, #5, and #6 below for an arbitrarily table-chosen altcoin called Dash to demonstrate how BIPs 32, 38, 39 and 44 can be tightly integrated with minor extensions to coherently support altcoins. It is very important for wallet developers to understand the concepts being espoused here to minimize wallet complexity while supporting multiple currencies simultaneously using a common BIP 32 hierarchical deterministic (HD) framework. 

The accuracy of portions of this table are not absolute (currently ~90% accuracy with strong source code trace-ability) until vetted by others, but the pattern for how it applies to altcoins is well understood. This table extends and complements [SLIP 44] (http://doc.satoshilabs.com/slips/slip-0044.html) referenced within [BIP44] (https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#registered-coin-types). This table also complements the [List of Address Prefixes](https://en.bitcoin.it/wiki/List_of_address_prefixes) top Table's "Hex" Column for row entries containing two hex digits. 

#### BIP44 Altcoin Version Mapping Table
```
      |   BIP 44     |     mainnet     |     mainnet     |     mainnet     |   
Coin  | (coin_type’) |   version/WIF   |  version/p2pkh  |  version/p2sh   |   References
———————————————————————————————————————————————————————————————————————————————————————————————————————————————————
BTC   |       0      |       128       |   0/('1')       |   5/('3')       |   https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp#L104
TEST  |       1      |       239       | 111/('m' | 'n') | 196/('2')       |   https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp#L177
LTC   |       2      |       176       |  48/('L')       |   5/('3')       |   https://github.com/litecoin-project/litecoin/blob/master-0.10/src/chainparams.cpp#L164
DOGE  |       3      |       158       |  30/('D')       |  22/('9' | 'A') |   https://github.com/dogecoin/dogecoin/blob/master/src/chainparams.cpp#L132
RDD   |       4      |       189       |  61/('R')       |   5/('3')       |   https://github.com/reddcoin-project/reddcoin/blob/master/src/base58.h#L275
DASH  |       5      |       204       |  76/('X')       |  16/('7')       |   https://github.com/dashpay/dash/blob/master/src/chainparams.cpp#L168
PPC   |       6      |       183       |  55/('P')       | 117/('p')       |   https://github.com/super3/Peercoin.net -   see NBT base58.h
NMC   |       7      |       180       |  52/('M' | 'N') |  13/('6')       |   https://github.com/domob1812/namecore/blob/master/src/chainparams.cpp#L133
FTC   |       8      |       142       |  14/('6' | '7') |   5/('3')       |   https://github.com/FeatherCoin/Feathercoin/blob/master-0.8/src/base58.h#L275
XCP   |       9      |    color_BTC    |   0/('1')       |       ?         |   Built on BTC, https://github.com/CounterpartyXCP/counterparty-lib  http://counterparty.io/docs/create_addresses/
BLK   |      10      |       153       |  25/('B')       |  85/('b')       |   https://github.com/rat4/blackcoin/blob/master/src/chainparams.cpp#L91
NSR   |      11      |     149/191 c/u |  63/('S')       |  64/('S' | 'T') |   Built on PPC, https://nubits.com/nushares/introduction
NBT   |      12      |     150/191 c/u |  25/('B')       |  26/('B')       |   https://bitbucket.org/JordanLeePeershares/nubit/NuBit / src /base58.h
MZC   |      13      |       224       |  50/('M')       |   9/('4' | '5') |   https://github.com/MazaCoin/MazaCoin/blob/master/src/chainparams.cpp#L76
VIA   |      14      |       199       |  71/('V')       |  33/('E')       |   https://github.com/viacoin/viacoin/blob/master/src/chainparams.cpp#L154
XCH   |      15      |    color_VIA    |  71/('V')       |       ?         |   Built on VIA, https://github.com/ClearingHouse/clearinghoused/blob/master/lib/config.py#L55 
RBY   |      16      |       189       |  61/('R')       |  85/('b')       |   https://github.com/rubycoinorg/rubycoin/blob/master/src/base58.h
GRS   |      17      |       176       |  36?/('F')      |   5/('3')       | https://github.com/GroestlCoin/groestlcoin/blob/master/src/chainparams.h#L38??? and  https://github.com/GroestlCoin/Groestlcoin-WPF/blob/master/coin-chains.xml (AddressVersion is 36)
DGC   |      18      |       158       |  30/('D')       |   5/('3')       |   https://github.com/DGCDev/digitalcoin/blob/master/src/chainparams.cpp#L74
CCN   |      19      |       156       |  28/('C')       |   5/('3')       |   https://github.com/Cannacoin-Project/Cannacoin/blob/Proof-of-Stake/src/base58.h#L275
DGB   |      20      |       128       |  30/('D')       |   5/('3')       |   https://github.com/digibyte/digibyte/blob/master/src/chainparams.cpp#L73
OA?   |      21      |  color_any_coin |  19/'a'(168bits)|  23/('A')       |   echo '18E14A7B6A307F426A94F8114701E7C8E774E7F9A47E2C2035DB29A206321725' | bx ec-to-public -u | bx bitcoin160 => Yields  010966776006953d5567439e5e39f86a0d273bee or 16UwLL9Risc3QfPqBUvKofHmBQ7wMtjvM
      |              |                 |                 |                 |   https://github.com/OpenAssets/open-assets-protocol/blob/master/address-format.mediawiki#example ( % echo '00010966776006953d5567439e5e39f86a0d273bee' | bx base58check-encode -v 19  =>  168 bit input Yields Open Assets Address: akB4NBW9UuCmHuepksob6yfZs6naHtRCPNy )
      |              |                 |                 |                 |   https://github.com/OpenAssets/open-assets-protocol/blob/master/specification.mediawiki#protocol-overview ( % echo 'dup hash160 [ 010966776006953D5567439E5E39F86A0D273BEE ] equalverify checksig' | bx script-encode | bx sha256 | bx ripemd160 | bx base58check-encode -v 23  =>  Yields Open Assets ID: ALn3aK1fSuG27N96UGYB1kUYUpGKRhBuBC  )
MONA  |      22      |       176       |  50/('M')       |   5/('3')       |   https://github.com/monacoinproject/monacoin/blob/master-0.10/src/chainparams.cpp#L159
CLAM  |      23      |                 | 137/('x')       |   5/('3')       |   https://github.com/nochowderforyou/clams/blob/master/src/base58.h#L277
XPM   |      24      |       151?      |  23/('A')       |  83/('a')       |   https://github.com/primecoin/primecoin/blob/master/src/base58.h#L275
NEOS  |      25      |       239       |  63/('S')       | 188/('2')       |   https://github.com/bellacoin/neoscoin/blob/master/src/chainparams.cpp#L123
JBS   |      26      |       171?      |  43/('J')       | 105/('j')       |   https://github.com/jyap808/jumbucks/blob/master/src/base58.h#L276
ZRC   |      27      |       208       |  80/('Z')       |   5/('3')       |   https://github.com/ZiftrCOIN/ziftrcoin/blob/master/src/chainparams.cpp#L159
VTC   |      28      |       199?      |  71/('V')       |   5/('3')       |   https://github.com/vertcoin/vertcoin/blob/master/src/base58.h#L275
NXT   |      29      |                 |                 |                 | https://bitbucket.org/JeanLucPicard/nxt/src and unofficial at https://github.com/Blackcomb/nxt
MUE   |      31      |                 |                 |                 | https://github.com/MonetaryUnit
ZOOM  |      32      |                 |                 |                 | https://github.com/zoom-c/
VPN   |      33      |       199?      |  71/('V')       |   5/('3')       |   https://github.com/Bit-Net/VpnCoin/blob/master/src/base58.h#L279
CDN   |      34      |       156?      |  28/('C')       |   5/('3')       |   https://github.com/ThisIsOurCoin/canadaecoin/blob/master/src/base58.h#L275
SDC   |      35      |       191       |  63/('S')       | 125/('s')       |   https://github.com/ShadowProject/shadow/blob/master/src/chainparams.cpp#L155
PKB   |      36      |                 |  55/('P')       |  28/('C')       |   https://github.com/parkbyte/ParkByte/blob/master/src/base58.h#L278
PND   |      37      |                 |  55/('P')       |  22/('9' | 'A') |   https://github.com/coinkeeper/2015-04-19_21-22_pandacoin/blob/master/src/base58.h#L279
NVC   |      50      |       136?      |   8/('4')       |  20/('9')       |   https://github.com/novacoin-project/novacoin/blob/master/src/base58.h#L280
DOGED |      77      |       158?      |  30/('D')       |  33/('E')       |   https://github.com/doged/dogedsource/blob/master/src/base58.h#L279
```

An empirical trend within the table above is that version/WIF values range between 128 and 255 inclusive. Similarly, version/p2pkh values range between 0 and 127 inclusive. Both the version/p2pkh and version/p2sh columns are typically for addresses 160 bits in length.  A notable exception is for the Open Assets row where the version/p2pkh address is 168 bits in length.  Both the version/p2pkh and version/p2sh columns contain information about base58check-encode starting address character for a cell version value.

General bx rules for commands supporting **--version (-v)** values that are 8-bit numbers in base10/decimal format:

* Commands supporting version values associated with private key functionality for desired coin types will use values from the **version/WIF** column. 
* Commands supporting version values associated with single signature address functionality for desired coin types will use the **version/p2pkh** column. 
* Commands supporting version values associated with multi-signature address functionality for desired coin types will use the **version/p2sh** column. 

It is anticipated this libbitcoin approach should be able to synthesize EC private keys and addresses for 100+ altcoins. Certainly there will be BIP/SLIP 44 registered coin types where it will not be readily apparent or appropriate to apply existing bx commands to arrive at associated WIF keys and/or addresses, e.g., coins with raw key lengths greater than 256 bits, or use hashing algorithms other that ripemd160, sha256, and sha512. Additionally, there will be altcoins that are not BIP/SLIP 44 registered that will have associated version/WIF and version/p2pkh values enabling bx to easily create private EC keys and associated addresses. Such unregistered coin types will be included in the table above, but each have a "coin type" not registered (NR) annotation.  If the libbitcoin framework is adopted by developers, it will naturally enable extended BIP 38 support for those altcoins listed in the table above. 

Finally, as a countermeasure to protect the Bitcoin cryptocurrency child prodigy as it grows through pubescence, and to provide a foundation to jump start the establishment of numerous multi-coin wallet implementations, emphasis will first be applied towards populating the table above for coins that are BIP/SLIP 44 registered. It is anticipated once Bitcoin protocols(s) maturation/growth phase is completed, there will be a strong delineation between payment and settlement network processing layers that will implicitly support different levels of trust, with the settlement layer providing a greater amount of uncensored trust and one or more scalable payment layers.

*It might be a bit much to digest at this point, but there are three additional columns technically required which are: testnet version/WIF, testnet version/p2pkh, and testnet version/p2sh. (Albeit, having a testnet for a Testnet might seem redundant...)  Further investigations are being performed to determine if other table columns are required to adequately support stealth addresses.*

### [bx - Wallet Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Wallet-Commands)

The table above is a "Rosetta Stone" for translating Bitcoin Elliptic Curve (EC) private keys and associated public addresses to those used by a number of altcoins having strong Bitcoin key/address synthesis heritage. This cryptocurrency Rosetta Stone currently provides important **--version (-v)** values for the following **bitcoin-explorer** wallet command used to be used to create addresses for altcoins:

* **[ec-to-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-address)**  ( use version/p2pkh column for addresses )


**1) Combined BIP 32 and 44 CLI Example Set:** *Apply M/44’/5’/0’/0/0 to create a compressed Dash public addresses for up to 4 billions addresses for safe use by an online machine!!!*

**A.** Be very afraid to use the weak brain wallet driven command sequence below on a computer that is online! Even with a very high entropy brain wallet, the approach below will will certainly be hacked unless you are a "cross domain solution" expert or apply multi-signature technology as risk mitigators. However, this example is provided for explanation continuity purposes for examples 1B and 1C below.
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-public  -i 0 | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76
```
```   
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2
```

**B.** Is an equivalent M/44’/5’/0’/0 extended public key approach that protects the confidentiality of the master seed. The extended public key that is part of the echo command below must be created on an offline computer. However, don't be afraid to apply the extended public key command sequence approach below to online computers. However, for privacy reasons, don't share extended keys beginning with xpub for Bitcoin or tpub for Testnet. 
```
% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76
```
```
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2
``` 

If crypto-currencies become more widely adopted, the approach above could severely diminish the need for eCommerce PCI-DSS compliance. This is a feature of permission-less blockchain technology! Permission-less blockchains don't require identity information to be utilized. This means permission-less cryptocurrency networks will naturally protect consumers from transaction payment identity theft for eCommerce transactions using a cryptocurrency transaction as payment/settlement. However, eCommerce servers accepting cryptographic currency payments utilizing such extended public keys must still protect the integrity of such extended public keys.  Otherwise, an eCommerce merchant risks customer payments being stolen or burned.

It is also worth noting that a number of altcoins have already defined their own unique extended key prefixes, e.g., Dash (xprv/xpub), forked LTC (Ltpv/Ltub) and DOGE (dgpv/dgub) implementations. However, the application of wrong prefixes won't interfere with the synthesis of proper types of EC private/public keys or addresses as long as "--version (-v)" values are applied correctly. The prefix tpub above resulted from compiling bx with the "--enable-testnet" flag. Not compiling bx with this flag will results in a similar extended public key starting with xpub. 


**C.** Demonstrates the generation of the next eCommerce Dash payment address (i.e., M/44’/5’/0’/0/1) to be applied by shopping cart checkout or point of sale (PoS) mechanisms, from the very same public extended key above (i.e., M/44’/5’/0’/0).
```
% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 1 | bx hd-to-ec | bx ec-to-address -v 76
```
```
XpTtgbcURSBfcuo8FZsNFeGrsCSi3jarAi
```


**2) BIP 39 Compliant CLI Example Set:** *Create master seeds in Spanish from a common weak English brainwallet seed requiring the memorization of 15, 24 or 48 words.* The BIP 39 functionality demonstrated here should be altcoin insensitive. The results below (i.e., 2B, 2D, 2F) makes a case that the more BIP 39 words, used from various spoken [languages](https://github.com/bitcoin/bips/blob/master/bip-0039/bip-0039-wordlists.md), applied to create a deterministic BIP 32 master key don't necessarily mean greater security...

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


**3) BIP 39 Compliant CLI Example:** *Recreate a master seed from BIP 39 words.* The BIP 39 functionality demonstrated here should be altcoin insensitive.
```
% echo 'enable load garage hard diagram trim nothing exclude fantasy gold ramp fiber wise ball have hero toddler spy excite glue maze drill else sell' | bx mnemonic-to-seed -p TREZOR
```
```
f0e63d191d75d39b5d1d8d1ae8ff1c48e51cacffb6d3881f31715572a59f352d35fa44a7e84f9a69712b206b9e04966a5794470993516e1b363a001fc3917f69
```

The following bitcoin explorer wallet commands are natural candidates to be extended to accommodate **--version (-v)** values:

* **[ec-to-wif](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-wif)**          ( recommend using version/WIF column for private keys )
* **[hd-to-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-hd-to-address)**      ( recommend using version/p2pkh column for addresses )
* **[hd-to-wif](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-hd-to-wif)**          ( recommend using version/WIF column for private keys )


### [bx - Encoding Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Encoding-Commands)

Most encoding commands supporting **--version** are not restricted as to which columns to use since these commands can be used to develop WIF private keys, associated coin single and multisig addresses, single signature stealth addresses, and possibly multisig stealth addresses. The following bitcoin explorer "encoding commands" provide version support:

* **[address-embed](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-address-embed)** ( no rules(s) yet for which version column(s) to apply )
* **[address-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-address-encode)** ( use version/p2pkh column for single signature addresses, version/p2sh column for creating multisig addresses, single signature stealth addresses???, multisig stealth addresses??? )
* **[base58check-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-base58check-encode)** ( use version/WIF column for private keys, version/p2pkh column for single signature addresses )
* **[wrap-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-wrap-encode)** ( use version/WIF column for private keys, version/p2pkh column for single signature addresses, version/p2sh column for multisig addresses )

The following bitcoin-explorer encoding command **should not** be extended to accommodate a **--version (-v)** value:

* **[script-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-script-encode)** ( For a basis to establish a rationale, see this [example](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-script-encode#example-3-creating-multi-signature-addresses).) 


**4) Combined BIP 32 and 44 Compliant CLI Example Set:** *Apply m/44’/5’/0’/0/0 example to create a compressed Dash private key.*

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


**5) Extended AES256Encrypt and AES256Decrypt BIP 38 CLI Example Set:** *For a Dash base16-encoded 256-bit secret elliptic curve key.*

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


**6) Extended "EC Multiply Mode" BIP 38 CLI Example Set:** *For Dash having an initial secret of 'knock knock', seed, salt, lot number of 0, and sequence number of 0. (Please note the information below needs to be cross correlated with security [recommendations](https://github.com/libbitcoin/libbitcoin/wiki/BIP38-Security-Considerations#recommendations) to arrive at a good processes for outsourcing the minting of coins or engraving of notes by owners of Dash funds.)*

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

It is very important to understand that minted/(engraved) coins/(notes) using a mechanism like the one described immediately above will not generally be transferable to 3rd parties without considerable trust between the original owner/curator of the minted/(engraved) coins/(notes) and downstream parties gaining physical possession (9/10th of ownership) of such coins/(notes). Without a form cryptographic "bonding", the lack of trust by most secondhand coin/(note) holders will naturally invoke a "bearer bond" behavior of others desiring to take full control of the value tied to this physical instrument's private key.

For risk reasons, this will cause secondhand coin/(note) holders to immediately break a coin's/note's seal to access its private key, and immediately "sweep"/(NOT IMPORT) this private key using an online wallet application.  This will cause a new blockchain P2PKH transaction to transfer cryptograhic monetary rights to a trusted private key of theirs.  This process severs previous immutable blockchain accounting value that was previously tied to such a physical coin or note, and it extrinsically becomes cryptographically worthless. Be aware that absolutely no cold storage trust should be given to any BIP 38 instrument that has "any history" of funds being spent. Numerous deposits being swept are fine, withdrawals absolutely not!

With the application of strong, high entropy, passwords/passphrases, BIP 38 functionality allows computer printing devices with untrusted firmware and network connections to safely print paper wallets for storage at multiple inconspicuous locations, not necessarily requiring the use of a safe of deposit boxes and possibly guard services.  Also, numismatic collectors can have very professional looking coins or notes minted or engraved by un-trusted minters or engravers if a BIP 38 "EC Multiply Mode" exchange protocol is utilized.  However, mints/engravers without "money transmitter" licenses need to take extra precautions to ensure their product is shipped before associated blockchain value can be attributed to it. One side effect of mints/engravers shipping product without being loaded is there are no initial branded assurances as to the accuracy of a coin's or note's cryptographic monetary value. 

In summary, both BIP 38 AES 256 bit encryption/decryption and EC Multiply mode can be used to create cold storage wallets for safe long-term keeping. There is the expectation from secondhand parties that minted/(engraved) coins/(notes) have blockchain "bearer bond" characteristics, and after taking possession will almost immediately be redeemed. If such coins/(notes) have tamper resistant secrets affixed to them to attain such a "bearer bond" characteristic, they must be physically guarded, an thus have associated commodity backwardation storage cost characteristics. 

Printing your own BIP 38 paper wallets with a trusted computer printer can engender greater privacy by helping to prevent others from ascertaining your cryptographic worth. It is also alright to keep BIP 38 paper wallets in multiple inconspicuous locations if they don't have monetary denominations printed on them, public addresses nor information printed on them indicating who the owner is or POCs are. This presents an interesting backwardation resistant characteristic for cryptocurrency savers that has never existed before in the physical world. If monetary denominations, public addresses or contact information is printed on BIP 38 wallets there will be an associated storage cost, but not as much as that for minted/(engraved) coins/(notes) with "bearer bond" characteristics.   


### [bx - Stealth Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Stealth-Commands)

The application **--version (-v)** values to **Stealth Commands** for altcoins is a work in progress...

The following bitcoin explorer wallet stealth commands are natural candidates to be extended to accommodate **--version (-v)** values:

* **[stealth-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-stealth-encode)** ( recommend using version/p2pkh column )
* *other stealth commands are under investigation*


### [bx - Transaction Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Transaction-Commands)

The following bitcoin-explorer transaction command is a natural candidate to be extended to accommodate a **--version (-v)** value:

* **[script-to-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-script-to-address)**  (recommend using version/p2sh column for multisig addresses)
