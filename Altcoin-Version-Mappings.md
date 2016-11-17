### Application of BIPs [32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), [38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki), [39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), [44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki), and [63 *(a work-in-progress)*](https://wiki.unsystem.net/en/index.php/DarkWallet/Stealth) to Altcoins

**Bitcoin-explorer's (bx)** command line interface (CLI), part of the libbitcoin tool suite, provides very substantial support for the following Bitcoin Improvement Proposals (BIP): 32, 38, 39, 44 and 63.  BIP 44 capabilities supporting alternative cryptocurrency coins (altcoins) results from how bx BIP 32 commands are piped to one another. The application of the BIP 44 related table below facilitates the extension of BIPS 32 and 38 to altcoins. Behaviors associated with using column version values from the first row of the "BIP44 Altcoin Version Mapping Table" below are integrated into bitcoin-explorer's commands as defaults. 

The libbitcoin team has a comprehensive understanding of this table's version values for the first row, Bitcoin (**BTC**), and has recently updated the bx CLI to support 100+ other altcoins. This awareness might create a common client-side code base, a merge, fostering convergence of existing Bitcoin altcoin code forks. However, such decisions will be at the discretion of altcoin main branch developers. Substantial server-side **bitcoin-server (bs)** node convergence opportunities will also emerge when libbitcoin supports *pluggable consensus modules*, but this Wiki article only mentions this concept for a later article.

The table below is a work-in-progress, but when completed will become an exemplar, providing important **"--version (-v)"** values.  The utility of these values is demonstrated by example sets #1, #4, #5, and #6 below for the **DASH** altcoin (row entry 6, or coin type 5) to demonstrate how BIPs 32, 38, 39 and 44 can be tightly integrated with minor extensions to coherently support altcoins using a unified codebase. It is very important for wallet developers to understand the concepts being espoused here to minimize wallet complexity while supporting multiple currencies simultaneously using a common BIP 32 hierarchical deterministic (HD) framework. 

The accuracy of portions of this table are not absolute (currently ~90% accuracy, with strong source code URL trace-ability to the right) until vetted by others, but the pattern for its application to altcoins is well understood. The table below extends and complements [SLIP 44] (https://github.com/satoshilabs/slips/blob/master/slip-0044.md) referenced within [BIP44] (https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki). The table below also complements the [List of Address Prefixes](https://en.bitcoin.it/wiki/List_of_address_prefixes) top Table's "Hex" column for row entries containing two hex digits.  

#### BIP44 Altcoin Version Mapping Table
```
      |  BIP 44    |      mainnet     |     mainnet     |     mainnet     |  EXT_SECRET_KEY   |
Coin  | coin_type’ |    version_WIF   |  version_p2pkh  |  version_p2sh   | version_hd_secret | References
———————————————————————————————————————————————————————————————————————————————————————————————————————————————————
BTC   |      0     |        128       |   0/('1')       |   5/('3')       | 76066276/('xprv') | https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp#L104
TEST  |      1     |        239       | 111/('m' | 'n') | 196/('2')       | 70615956/('tprv') | https://github.com/bitcoin/bitcoin/blob/master/src/chainparams.cpp#L177
LTC   |      2     |        176       |  48/('L')       |   5/('3')       | 76066276/('xprv') | https://github.com/litecoin-project/litecoin/blob/master-0.10/src/chainparams.cpp#L164
DOGE  |      3     |        158       |  30/('D')       |  22/('9' | 'A') | 49988504/('dgpv') | https://github.com/dogecoin/dogecoin/blob/master/src/chainparams.cpp#L132
RDD   |      4     | 189/'V'/c        |  61/('R')       |   5/('3')       | 76066276/('xprv') | https://github.com/reddcoin-project/reddcoin/blob/master/src/base58.h#L275 & https://github.com/reddcoin-project/rddnet/blob/master/params.go#L148
DASH  |      5     |        204       |  76/('X')       |  16/('7')       | 50221772/('drkp') | https://github.com/dashpay/dash/blob/master/src/chainparams.cpp#L168
PPC   |      6     |        183       |  55/('P')       | 117/('p')       |                   | https://github.com/belovachap/peercoin/blob/master/src/base58.h#L267 and https://github.com/super3/Peercoin.net -   see NBT base58.h
NMC   |      7     |        180       |  52/('M' | 'N') |  13/('6')       | 76066276/('xprv') | https://github.com/domob1812/namecore/blob/master/src/chainparams.cpp#L133
FTC   |      8     |        142       |  14/('6' | '7') |   5/('3')       |                   | https://github.com/FeatherCoin/Feathercoin/blob/master-0.8/src/base58.h#L275
XCP   |      9     |     color_BTC    |   0/('1')       |       ?         |                   | Built on BTC, https://github.com/CounterpartyXCP/counterparty-lib  http://counterparty.io/docs/create_addresses/
BLK   |     10     |        153       |  25/('B')       |  85/('b')       | 76066276/('xprv') | https://github.com/rat4/blackcoin/blob/master/src/chainparams.cpp#L91
NSR   |     11     |     149/191 c/u  |  63/('S')       |  64/('S' | 'T') |                   | Built on PPC, https://nubits.com/nushares/introduction
NBT   |     12     |     150/191 c/u  |  25/('B')       |  26/('B')       |                   | https://bitbucket.org/JordanLeePeershares/nubit/NuBit / src /base58.h
MZC   |     13     |        224       |  50/('M')       |   9/('4' | '5') |      unknown      | https://github.com/MazaCoin/MazaCoin/blob/master/src/chainparams.cpp#L76
VIA   |     14     |        199       |  71/('V')       |  33/('E')       | 76066276/('xprv') | https://github.com/viacoin/viacoin/blob/master/src/chainparams.cpp#L154
XCH   |     15     |     color_VIA    |  71/('V')       |       ?         |                   | Built on VIA, https://github.com/ClearingHouse/clearinghoused/blob/master/lib/config.py#L55 
RBY   |     16     |        189       |  61/('R')       |  85/('b')       |                   | https://github.com/rubycoinorg/rubycoin/blob/master/src/base58.h
GRS   |     17     |        128       |  36/('F')       |   5/('3')       | 76066276/('xprv') | https://github.com/GroestlCoin/groestlcoin/blob/master/src/groestlcoin.cpp#L380
DGC   |     18     |        158       |  30/('D')       |   5/('3')       | 76066276/('xprv') | https://github.com/DGCDev/digitalcoin/blob/master/src/chainparams.cpp#L74
CCN   |     19     |        156       |  28/('C')       |   5/('3')       |                   | https://github.com/Cannacoin-Project/Cannacoin/blob/Proof-of-Stake/src/base58.h#L275
DGB   |     20     |        128       |  30/('D')       |   5/('3')       | 76066276/('xprv') | https://github.com/digibyte/digibyte/blob/master/src/chainparams.cpp#L73
???   |     21     |  color_agnostic  |  19/'a'(168bits)|  23/('A')       |                   | See "Open Assets Test Vector Examples" below
MONA  |     22     |        176       |  50/('M')       |   5/('3')       | 76066276/('xprv') | https://github.com/monacoinproject/monacoin/blob/master-0.10/src/chainparams.cpp#L159
CLAM  |     23     |        133       | 137/('x')       |  13/('6')       | 76066276/('xprv') | https://github.com/nochowderforyou/clams/blob/master/src/chainparams.cpp#L97
XPM   |     24     |        151       |  23/('A')       |  83/('a')       |                   | https://github.com/primecoin/primecoin/blob/master/src/base58.h#L275
NEOS  |     25     |        239       |  63/('S')       | 188/('2')       |      unknown      | https://github.com/bellacoin/neoscoin/blob/master/src/chainparams.cpp#L123
JBS   |     26     |        171       |  43/('J')       | 105/('j')       |                   | https://github.com/jyap808/jumbucks/blob/master/src/base58.h#L276
ZRC   |     27     |        208       |  80/('Z')       |   5/('3')       | 76066276/('xprv') | https://github.com/ZiftrCOIN/ziftrcoin/blob/master/src/chainparams.cpp#L159
VTC   |     28     |        199       |  71/('V')       |   5/('3')       |                   | https://github.com/vertcoin/vertcoin/blob/master/src/base58.h#L275
NXT   |     29     |                  |                 |                 |                   | https://bitbucket.org/JeanLucPicard/nxt/src and unofficial at https://github.com/Blackcomb/nxt
MUE   |     31     |        143       |  15/('7')       |   9/('4' | '5 ) |1297433939/('HRBy')| https://github.com/MonetaryUnit/MUE-Src/blob/master/src/chainparams.cpp#L221
ZOOM  |     32     |        231       | 103/('i')       |  92/('e')       |                   | https://github.com/zoom-c/zoom/blob/master/src/base58.h#L275
VPN   |     33     |        199       |  71/('V')       |   5/('3')       |                   | https://github.com/Bit-Net/VpnCoin/blob/master/src/base58.h#L279
CDN   |     34     |        156       |  28/('C')       |   5/('3')       |                   | https://github.com/ThisIsOurCoin/canadaecoin/blob/master/src/base58.h#L275
SDC   |     35     |        191       |  63/('S')       | 125/('s')       |4001378792/('sdcv')| https://github.com/ShadowProject/shadow/blob/master/src/chainparams.cpp#L164
PKB   |     36     |        183       |  55/('P')       |  28/('C')       |                   | https://github.com/parkbyte/ParkByte/blob/master/src/base58.h#L278
PND   |     37     |        183       |  55/('P')       |  22/('9' | 'A') |                   | https://github.com/coinkeeper/2015-04-19_21-22_pandacoin/blob/master/src/base58.h#L279
START |     38     |        253       | 125/('s')       |   5/('3')       |                   | https://github.com/startcoin-project/startcoin/blob/master/src/base58.h#L275
GCR   |     39     |        154       |  38/('G')       |  97/('g')       | 76066276/('xprv') | https://github.com/globalcurrencyreserve/gcr/blob/master/src/chainparams.cpp#L88
NVC   |     50     |        136       |   8/('4')       |  20/('9')       |                   | https://github.com/novacoin-project/novacoin/blob/master/src/base58.h#L280
AC    |     51     |        151       |  23/('A')       |   8/('4')       |                   | https://github.com/AsiaCoin/AsiaCoinFix/blob/master/src/base58.h#L279
BTCD  |     52     |        188       |  60/('R')       |  85/('b')       |                   | https://github.com/jl777/btcd/blob/master/src/base58.h#L278
DOPE  |     53     |        136       |   8/('4')       |   5/('3')       |                   | https://github.com/dopecoin-dev/DopeCoinV3/blob/master/src/base58.h#L279
TPC   |     54     |        193       |  65/('T')       |   5/('3')       |                   | https://github.com/9cat/templecoin/blob/templecoin/src/base58.h#L275
???   |     55     |        151       |  23/('A')       |   5/('3')       |                   | https://github.com/iobond/aib/blob/master/src/base58.h#L276 and from ./aib/src/wtmint.h for #define WTMINT_PUBKEY_ADDRESS 23 // Dec.
ETH   |     60     |                  |                 |                 |                   | https://github.com/ethereum/  and https://github.com/ethereum/cpp-ethereum/wiki
???   |     64     |                  |                 |                 |                   | https://github.com/openchain/
OK    |     69     |        183       |  55/('P')       |  28/('C')       | 63708275/('okpv') | https://github.com/okcashpro/okcash/blob/master/src/chainparams.cpp#L168
DOGED |     77     |        158       |  30/('D')       |  33/('E')       |                   | https://github.com/doged/dogedsource/blob/master/src/base58.h#L279
EFL   |     78     |        176       |  48/('L')       |   5/('3')       |                   | https://github.com/Electronic-Gulden-Foundation/egulden/blob/master/src/base58.h#L275
POT   |     81     |        183       |  55/('P')       |   5/('3')       |                   | https://github.com/potcoin/Potcoin/blob/master/src/base58.h#L275
XRP   |     NR     | 96?/'s'(116 bits)|96?/'r'(136 bits)|                 |                   | https://github.com/stevenzeiler/ripple-wallet (OMG - Is Ripple using 96 bit secret keys?)
XMR   |    128     |        N/A       |    /('4')       |    N/A          |  ???              |
ZEC   |    133     |        128       | (28 & b8)/('t1')| (28 & bd)/('t3')| 76066276/('xprv') | https://github.com/zcash/zcash/blob/master/src/chainparams.cpp#L105
```

An empirical trend within the table above is that version_WIF values range between 128 and 255 inclusive. Similarly, version_p2pkh values range between 0 and 127 inclusive. A noticeable  exception is for CLAM. Both the version_p2pkh and version_p2sh columns are typically for addresses 160 bits in length.  Notable exceptions are annotated for the Open Assets row where the version_p2pkh address is 168 bits in length, and Ripple (XRP) having 136 bits.  Both the version_p2pkh and version_p2sh columns also contain information about base58check-encode starting address characters for a cell's version value.  As long as the addresses are precisely 160 bits in length, such values also align with the lower table from the [List of Address Prefixes](https://en.bitcoin.it/wiki/List_of_address_prefixes).

General bx rules for commands supporting **--version (-v)** values that are 8-bit numbers in base10/decimal format:

* Commands supporting version values associated with private key functionality for desired coin types will use values from the **version_WIF** column. Notable exceptions to this rule are are for **ec-to-ek** and **ek-new**. All "ek" related bx commands use the **version_p2pkh** column.
* Commands supporting version values associated with single signature address functionality for desired coin types will use the **version_p2pkh** column. 
* Commands supporting version values associated with multi-signature address functionality for desired coin types will use the **version_p2sh** column.
* The **hd-new** command enables a hierarchical deterministic *extended private key* prefix to be set by using the value from the **version_hd_secret** column.  

It is anticipated this libbitcoin approach should be useful for synthesizing elliptic curve (EC) private keys, EC public keys, and addresses for 100+ altcoins. Certainly, there will be BIP/SLIP 44 registered coin types where it will not be readily apparent or appropriate to apply existing bx commands to arrive at associated WIF keys and/or addresses, e.g., use of hashing algorithms other than ripemd160, sha256, and sha512 such as Keccak sha3 technologies. Additionally, there will be altcoins that are not BIP/SLIP 44 registered that will have associated version_WIF and version_p2pkh values enabling bx to easily create private EC keys and associated addresses. Such unregistered coin types will be included in the table above, but each have a "coin type" annotation of "not registered" (NR).  If client-side libbitcoin framework is adopted by developers, it will naturally enable extended BIP 38 support for those altcoins listed in the table above with significantly less overloading the "6P" encrypted EC private key prefix reserved for Bitcoin. 

Finally, as a countermeasure to protect the Bitcoin cryptocurrency child prodigy as it grows through its pubescence phase, and to provide a foundation to jump start the establishment of numerous multi-coin wallet implementations, emphasis will first be applied towards populating the table above for altcoins that are BIP/SLIP 44 registered. It is anticipated once Bitcoin protocols(s) maturation/growth phase is completed, there will be a strong delineation between payment and settlement network processing layers that will implicitly support different levels of trust - with a blockchain settlement layer providing a greater amount of uncensored trust, and one or more payment mechanisms supporting greater scalability.

### bx - Settings

The examples (i.e., 1 through 6) provided below for DASH in this Wiki article were chosen to function with the bitcoin-explorer etc/libbitcoin/bx.cfg file settings bundled with the bx package. This package bundled configuration file is tailored for Bitcoin (BTC). The environmental variable BX_CONFIG is frequently used to set the path of where a customized configuration file, such as bx.cfg, is saved that will override compiled bx defaults. Explicitly setting bx CLI **--version (-v)** values will override settings provided by a bx configuration file, e.g., bx.cfg. 

The intent here is to briefly touch upon six important [wallet](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-settings) configuration settings that influence altcoin client-side behaviors. To tailor the bx configuration file for DASH, the six bullet settings below are provided. Strong source code traceability back to DASH code base is provided below as hyperlinks.

* wif_version = [204](https://github.com/dashpay/dash/blob/master/src/chainparams.cpp#L170)
* pay_to_public_key_hash_version = [76](https://github.com/dashpay/dash/blob/master/src/chainparams.cpp#L168)
* pay_to_script_hash_version = [16](https://github.com/dashpay/dash/blob/master/src/chainparams.cpp#L169)
* hd_private_version = [50221772](https://github.com/dashpay/dash/blob/master/src/chainparams.cpp#L172)
* hd_public_version = [50221816](https://github.com/dashpay/dash/blob/master/src/chainparams.cpp#L171)
* transaction_version = 1

The EXT_SECRET_KEY DASH source code variable set to 0x02FE52CC is base16 encoded (or 50221772 in base10), and this numerical prefix causes DASH extended private keys to always start with "drkp". The EXT_PUBLIC_KEY DASH source code variable set to 0x02FE52F8 is base16 encoded (or 50221816 in base10), and this numerical prefix causes DASH extended private keys to always start with "drkv". Most altcoins have yet to customize such BIP 32 extended key prefix settings, and using prefixes for BTC and TEST don't really influence the net key synthesis results for altcoins. Hence, the examples for synthesizing DASH private keys and public addresses below will not utilize setting values 50221772 and 50221816. Finally, most alcoins with strong Bitcoin heritage are using transaction messaging format version 1.  

### [bx - Wallet Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Wallet-Commands)

The table above is a "Rosetta Stone" for translating Bitcoin EC private keys and associated public keys and addresses to those used by a number of altcoins having strong Bitcoin key/address synthesis heritage. This cryptocurrency Rosetta Stone currently provides important **--version (-v)** values for the following **bitcoin-explorer** wallet commands:

* **[ec-to-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-address)**  ( use version_p2pkh column for addresses )
* **[ec-to-wif](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-wif)**          ( use version_WIF column for private keys )


**1) Combined BIP 32 and 44 CLI Example Set:** *Apply M/44’/5’/0’/0/0 to create a compressed DASH public addresses for up to 4 billions addresses for safe use by an online machine!!!*

**A.** Be very afraid to use the weak brain wallet driven command sequence below on a computer that is online! Even with a very high entropy brain wallet, the approach below will will certainly be hacked unless you are a "cross domain solution" expert or apply multi-signature technology as risk mitigation. However, this brain wallet example is provided to enhance the understanding and repeatability of examples 1B and 1C below.
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-public  -i 0 | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76
```
```   
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2
```

**B.** Is an equivalent M/44’/5’/0’/0 extended public key approach (to "A" immediately above) that protects the confidentiality of the master seed. The extended public key that is part of the echo command below *must* be created on an offline computer. However, don't be afraid of applying the extended public key (starts with xpub) command sequence approach below to online computers. However, for privacy reasons, don't share extended keys beginning with *xpub* for the Bitcoin Mainnet or *tpub* for Bitcoin Testnet. 
```
% echo 'xpub6EVt68TrKV5YPXF9oXfEPsqWc5sRjLFQg7GAtLKwF4oss4sZKRvjQqNGYk4ZvrsC3hzuL87LvB7phibDDQSuCEeTRii4ST8Y28DuyfoFxJB' | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76
```
```
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2
``` 

If crypto-currencies become more widely adopted, the approach above will severely reduce the need for onerous eCommerce PCI-DSS compliance that is contractually required by credit card payment networks. This is a feature of permission-less blockchain technology! Permission-less blockchains don't require identity information to be utilized. This means permission-less cryptocurrency networks will naturally protect consumers from transaction payment identity theft for eCommerce transactions using a cryptocurrency transaction as payment/settlement. However, eCommerce servers accepting cryptographic currency payments utilizing such extended public keys must still protect the integrity of such extended public keys.  Otherwise, eCommerce merchants risks customer payments being stolen or burned. *Burned addresses* are ones for which the associated EC private keys are not known. 

It is also worth noting that a number of altcoins have already defined their own unique extended key prefixes, e.g., DASH (drkp/drkv), forked LTC (Ltpv/Ltub) and DOGE (dgpv/dgub) implementations. However, the application of wrong altcoin extended key prefixes won't interfere with the synthesis of proper types of EC private/public keys or addresses as long as "--version (-v)" values are applied correctly.

**C.** Demonstrates the generation of the next eCommerce DASH payment address (i.e., M/44’/5’/0’/0/1) to be applied by shopping cart checkout or point of sale (PoS) mechanisms, from the very same public extended key above (i.e., M/44’/5’/0’/0).
```
% echo 'xpub6EVt68TrKV5YPXF9oXfEPsqWc5sRjLFQg7GAtLKwF4oss4sZKRvjQqNGYk4ZvrsC3hzuL87LvB7phibDDQSuCEeTRii4ST8Y28DuyfoFxJB' | bx hd-public  -i 1 | bx hd-to-ec | bx ec-to-address -v 76
```
```
XpTtgbcURSBfcuo8FZsNFeGrsCSi3jarAi
```


**2) BIP 39 Compliant CLI Example Set:** *Create master seeds in Spanish from a common weak English brainwallet seed requiring the memorization of 15, 24 or 48 words.* The BIP 39 functionality demonstrated here is altcoin insensitive. The results below (i.e., 2B, 2D, 2F) makes a case that more BIP 39 words, used from various spoken [languages](https://github.com/bitcoin/bips/blob/master/bip-0039/bip-0039-wordlists.md), applied to create a deterministic BIP 32 master key don't necessarily engender greater security...

**A.**  Create a seed for a 15 word representation for a BIP 39 encoded master seed.
```
% echo 'TREZOR' | bx base16-encode | bx ripemd160
```
```
0d7a259d0280785f98659ee9cb1809663cbd4672
```
**B.** 15 Spanish word BIP 39 representation of a master seed.
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx mnemonic-new -l es 0d7a259d0280785f98659ee9cb1809663cbd4672
```
```
anillo salón grosor afinar alacrán champú ganso pimienta todo fiel aceptar rojo rodar ombligo riñón
```

**C.** Create a seed for a 24 word representation for a BIP 39 encoded master seed.
```
% echo 'TREZOR' | bx base16-encode | bx sha256
```
```
91d5a6684b637ded1e0d9eb7fea85a864ac3a7c44d666c3254b76108ae201550
```
**D.** 24 Spanish word BIP 39 representation of a master seed.
```
echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx mnemonic-new -l es 91d5a6684b637ded1e0d9eb7fea85a864ac3a7c44d666c3254b76108ae201550
```
```
moler pausa nevar música conocer veinte júpiter pimienta pollo valor átomo ancho pasar seco arbusto pata hígado monto célebre raspa matriz aprender familia apoyo
```

**E.** Create a seed for a 48 word representation for a BIP 39 encoded master seed.
```
echo 'TREZOR' | bx base16-encode | bx sha512
```
```
4da2ce0586c67550f627d108d4b0352646add71253a1d647076f9ffa3b6d1379c6f6f4c8e49a185344ee272d1a66a185329686a42ef61bf08782d595fc313824
```
**F.** 48 Spanish word BIP 39 representation of a master seed.
```
echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx mnemonic-new -l es 4da2ce0586c67550f627d108d4b0352646add71253a1d647076f9ffa3b6d1379c6f6f4c8e49a185344ee272d1a66a185329686a42ef61bf08782d595fc313824
```
```
enredo ático litro ánimo grosor paella símbolo viejo aleta orgía ángulo encía hebra torpedo edificio invierno sermón copa sostén dedo opción pluma enseñar cordón velero orquesta coser clínica luz olfato pompa terror babor codo gancho gordo guía evitar proeza rechazo tubo cuchara pizca carta rebote nota mirar curioso
```


**3) BIP 39 Compliant CLI Example:** *Recreate a master seed from BIP 39 words.* The BIP 39 functionality demonstrated here is altcoin insensitive.
```
% echo 'enable load garage hard diagram trim nothing exclude fantasy gold ramp fiber wise ball have hero toddler spy excite glue maze drill else sell' | bx mnemonic-to-seed -p TREZOR
```
```
f0e63d191d75d39b5d1d8d1ae8ff1c48e51cacffb6d3881f31715572a59f352d35fa44a7e84f9a69712b206b9e04966a5794470993516e1b363a001fc3917f69
```


### [bx - Encoding Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Encoding-Commands)

Most encoding commands supporting **--version (-v)** are not restricted as to which columns to use since these commands can be used to develop WIF private keys, associated coin single & multisig addresses, single signature stealth addresses, and possibly multisig stealth addresses. The following bitcoin explorer "encoding commands" provide version support:

* **[address-embed](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-address-embed)** ( no rules(s) yet for which version column(s) to apply )
* **[address-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-address-encode)** ( use version_p2pkh column for single signature addresses, version_p2sh column for creating multisig addresses, single signature stealth addresses???, multisig stealth addresses??? )
* **[base58check-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-base58check-encode)** ( use version_WIF column for private keys, version_p2pkh column for single signature addresses )
* **[wrap-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-wrap-encode)** ( use version_WIF column for private keys, version_p2pkh column for single signature addresses, version_p2sh column for multisig addresses )

The following bitcoin-explorer encoding command **should not** be extended to accommodate a **--version (-v)** value:

* **[script-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-script-encode)** ( For a basis to establish a rationale, see Example 7C [Is equivalent to](https://github.com/libbitcoin/libbitcoin/wiki/Altcoin-Version-Mappings#is-equivalent-to) below.) 


**4) Combined BIP 32 and 44 Compliant CLI Example Set:** *Apply m/44’/5’/0’/0/0 example to create a compressed DASH private key.*

**A.** Synthesized compressed EC private key below is derived from a very weak cryptographical brain wallet. Note that this affords absolutely no protection of the master seed that feeds the hd-new.  The piped "sed 's/$/01/'" command below appends the private key with "01" to signal downstream public key software to create companion compressed EC public keys in a compressed format. Without this extra suffix, the EC public key will be in the uncompressed format that requires twice the memory of compressed keys. 
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204 
```
```                                                                    
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM
```

**B.** This m/44’/5’/0’/0 extended private key synthesis approach, derived from the same cryptographically weak brain wallet, also protects the confidentiality of the master seed.  However, extreme care must be exercised to protect the confidentiality of extended private keys starting with xprv for BTC or tprv for TEST. A compromise of the confidentiality of m/44’/5’/0’/0 for this DASH example will likely compromise the funds for up ~4 billion synthesized addresses.
```
% echo  'xprvA1WXgcvxV7XFB3AghW8E2jtn442wKsXZJtLa5wvKgjGtzGYQmtcUs33nhT4kWy7ARnWwnppyY79RQS7TjHYmvSeu1xWns9wEB81zLq34MjQ' | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204
```
```
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM
```

**C.** Uses the same m/44’/5’/0’/0 extended private key that protects the confidentiality of the master seed to create m/44’/5’/0’/0/1.
```
% echo 'xprvA1WXgcvxV7XFB3AghW8E2jtn442wKsXZJtLa5wvKgjGtzGYQmtcUs33nhT4kWy7ARnWwnppyY79RQS7TjHYmvSeu1xWns9wEB81zLq34MjQ' | bx hd-private -i 1 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204
```
```
XGobHujzvnXWdnteE2aZU8TH2EEgbWkXr9iFQuU9QL1mpU21brja
```

### [bx - Key Encryption Commands] (https://github.com/libbitcoin/libbitcoin-explorer/wiki/Key-Encryption-Commands)

The table above also complements [Altchain Encrypted Private Keys](https://github.com/libbitcoin/libbitcoin/wiki/Altchain-Encrypted-Private-Keys#sample-map) by supporting the following **bitcoin-explorer** "encrypted key" commands to **extend BIP 38 functionality** to altcoins:

* **[ec-to-ek](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-ek)** ( use version_p2pkh column for addresses )
* **[ek-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-address)**  ( use version_p2pkh column for addresses )
* **[ek-new](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-new)** ( use version_p2pkh column for addresses )
* **[ek-public](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-public)**  ( use version_p2pkh column for addresses )


**5) Extended AES256Encrypt and AES256Decrypt BIP 38 CLI Example Set:** *For a DASH base16-encoded 256-bit secret elliptic curve key.*

**A.** Extended BIP 38 (256 bit AES) encryption for DASH of a base16 encoded EC private key.
```
% bx ec-to-ek -v 76 'Hello it is me' f9a8f6d4a24b99d4944ee3db83c85383e9c13e85cb50ad60a9e1a96e02f6d269
```
```
7f7QjekuNesi3dJ9gE49bQSZAgJAuHB5u3ERLHebS7CEvAY43XTfAHvNfE
```
**B.** Extended BIP 38 (256 bit AES) decryption of an extended DASH BIP 38 encrypted base16 encoded EC private key.
```
% bx ek-to-ec 'Hello it is me' 7f7QjekuNesi3dJ9gE49bQSZAgJAuHB5u3ERLHebS7CEvAY43XTfAHvNfE
```
```
f9a8f6d4a24b99d4944ee3db83c85383e9c13e85cb50ad60a9e1a96e02f6d269
```


**6) Extended "EC Multiply Mode" BIP 38 CLI Example Set:** *For DASH having an initial secret of 'knock knock', seed, salt, lot number of 0, and sequence number of 0. (Please note the information below needs to be cross correlated with security [recommendations](https://github.com/libbitcoin/libbitcoin/wiki/BIP38-Security-Considerations#recommendations) to arrive at a good processes for outsourcing the minting of coins or engraving of notes by owners of DASH funds.)*

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

**D.** Is performed by the minter/engraver to know the BIP 38 encrypted private key to be publicly labelled on a DASH coin/note.
```
% bx ek-new -v 76 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```
```
7fNJEMECkTMvUtMZnYEmAyTiBdxvRTmNictRBvLK5vbNwbWDpJZMNSMCjH
``` 

**CP1.** Computed EC DASH private key - comparison point #1
```
% bx ek-to-ec 'knock knock' 7fNJEMECkTMvUtMZnYEmAyTiBdxvRTmNictRBvLK5vbNwbWDpJZMNSMCjH
```
```
cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23
```

**CP2.** Traditional computation of an EC DASH public key - comparison point #2
```
% echo 'cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23' | bx ec-to-public
```
```
035d37339d296b1a7ea8c7f04cf33eb0e8fd547df58d60259c9e4d9404795cd7f1
```

**CP3.** Traditional computation of the associated DASH address - comparison point #3
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

**G.** Is performed by a coin/note owner to double authenticate the DASH coin address where funds are to be deposited. There could be a typo mistake, cut-and-paste mistake, or a man-in-the-middle attack (e.g., from utilizing an untrusted communication channel between the minter/engraver and coin/note owner)  compromising the integrity of the confirmation code resulting in a bad address created by step 6F. If results match, a deposit is not likely to be lost or burned. Observe the result below matches CP3
```
% bx ek-address -v 76 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
```
```
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu
```

It is very important to understand that minted/(engraved) coins/(notes) using a mechanism like the one described immediately above will not generally be transferable to 3rd parties without considerable trust between the original owner/curator of the minted/(engraved) coins/(notes) and downstream parties gaining physical possession (9/10th of ownership) of such coins/(notes). Without a form of cryptographic "bonding", the lack of trust by most secondhand coin/(note) holders will naturally invoke a "bearer bond" behavior by others desiring to take full control of the value tied to such physical cryptographic private key.

For risk reasons, this will cause secondhand coin/(note) holders to immediately break a coin's/(note's) seal to access its private key, and immediately "sweep"/(NOT IMPORT) this private key using an online wallet application.  This will cause a new blockchain P2PKH transaction to transfer cryptograhic monetary rights to a separate trusted private key of theirs.  This process severs previous immutable blockchain accounting value that was previously tied to such a physical coin or note, and it extrinsically becomes cryptographically worthless. Be aware that absolutely no cold storage trust should be given to any BIP 38 instrument that has "any history" of funds being spent. Numerous deposits being swept are fine, withdrawals absolutely not because the funds will no longer be considered in cold storage!

With the application of strong, high entropy, passwords/passphrases, BIP 38 functionality allows computer printing devices with untrusted firmware and network connections to safely print paper wallets for storage at multiple inconspicuous locations, not necessarily requiring the use of a safe of deposit boxes and possibly guard services.  Also, numismatic collectors can obtain very professional looking coins or notes minted or engraved by un-trusted minters or engravers if a BIP 38 "EC Multiply Mode" exchange protocol is utilized.  However, mints/(engravers) without "money transmitter" licenses need to take extra precautions to ensure their product is shipped before associated blockchain value can be attributed to it. One side effect of mints/(engravers) shipping product without being loaded is there are no initial branded assurances as to the accuracy of a coin's or note's cryptographic monetary value. 

In summary, both BIP 38 AES 256 bit encryption and decryption along with BIP 38 EC Multiply Mode can be used to create cold storage wallets for safe long-term keeping. There is the expectation from secondhand parties that minted/(engraved) coins/(notes) have blockchain "bearer bond" characteristics, and after taking possession will almost immediately be redeemed. If such coins/(notes) have tamper resistant secrets affixed to them to attain such a "bearer bond" characteristic, they must be physically guarded, an thus have associated commodity backwardation storage cost characteristics. 

Printing your own BIP 38 paper wallets with a trusted computer printer can engender greater privacy by helping to prevent others from ascertaining your cryptographic worth. It is also alright to keep BIP 38 paper wallets in multiple inconspicuous locations if they don't have monetary denominations printed on them, public addresses nor information printed on them indicating who the owner is or POCs are. This presents an interesting backwardation resistant characteristic for cryptocurrency savers that has never existed before in the physical world. If monetary denominations, public addresses or contact information is printed on BIP 38 wallets there will be an associated storage cost, but not as much as that for minted/(engraved) coins/(notes) with "bearer bond" characteristics.   


### [bx - Stealth Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Stealth-Commands)

The following bitcoin-explorer "stealth command" provides a **--version (-v)** value interface for altcoin support:

* **[stealth-encode](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-stealth-encode)** ( use version_p2pkh column )


### [bx - Transaction Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Transaction-Commands)

The following bitcoin-explorer transaction command accommodates a **--version (-v)** value:

* **[script-to-address](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-script-to-address)**  (use version_p2sh column for multisig addresses)


### 7) Bitcoin (BTC) BIP 39/44 Technology Examples:

**Bitcoin WIF m/44'/0'/0'/0/0 Private Key:**
```
% echo "radar blur cabbage chef fix engine embark joy scheme fiction master release" | bx mnemonic-to-seed | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 0 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 128
```
```
KxdnUF9EAinLC6KWSrEZdQvdkT3XSbvDHzxANB1qKrpPjxSK2TFC
```

**Bitcoin M/44'/0'/0'/0/0 Public Address:**
```
% echo "radar blur cabbage chef fix engine embark joy scheme fiction master release" | bx mnemonic-to-seed | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 0 | bx hd-private -d -i 0 | bx hd-public -i 0 | bx hd-public -i 0 | bx hd-to-ec | bx sha256 | bx  ripemd160 | bx base58check-encode -v 0
```
```
1NAW6zzKT5zjtd73nVP86mtv1etp7GfThv
```


### 8) Dash (DASH) BIP 39/44 Technology Examples:

**Dash WIF m/44'/5'/0'/0/0 Private Key:**
```
% echo "radar blur cabbage chef fix engine embark joy scheme fiction master release" | bx mnemonic-to-seed | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204
```
```
XGnxUtxjfseCYWQvj8cbyvr3ec2QBApo6NGaSrX3nNJwc6qYD2ts
```

**Dash M/44'/5'/0'/0/0 Public Address:**
```
% echo "radar blur cabbage chef fix engine embark joy scheme fiction master release" | bx mnemonic-to-seed | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-public -i 0 | bx hd-public -i 0 | bx hd-to-ec | bx sha256 | bx  ripemd160 | bx base58check-encode -v 76
```
```
XhcMA4re1dVBUizBHRNE1VMXkBX8FkFbdV
```


### 9) Zcash (ZEC) BIP 39/44 Technology Examples:

**Zcash WIF m/44'/133'/0'/0/0 Private Key:** 
```
% echo "radar blur cabbage chef fix engine embark joy scheme fiction master release" | bx mnemonic-to-seed | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 133 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 128
```
```
KxPhnyg5qNmE4zRQxySHhPoHrhBhZYjPuqZB9pLDSvdbEtMvHjN3
```

**Zcash M/44'/133'/0'/0/0 Public Address:**
```
% echo "radar blur cabbage chef fix engine embark joy scheme fiction master release" | bx mnemonic-to-seed | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 133 | bx hd-private -d -i 0 | bx hd-public -i 0 | bx hd-public -i 0 | bx hd-to-ec | bx sha256 | bx  ripemd160 | sed 's/^/b8/' | bx base58check-encode -v 28
```
```
t1Zv78LE5HMXGCH1MfBcBzywHdAfosDv6tE
```


### 10) Monero (XMR) BIP 39/44 Technology Examples:

**Monero m/44'/128'/0' Account :**

```
% echo "radar blur cabbage chef fix engine embark joy scheme fiction master release" | bx mnemonic-to-seed | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 128 |  bx hd-private -d -i 0 | bx hd-to-ec | ./xmr
```
    Seed                 : e62551cad9fe0f05d7c84cf6a0ef7e8fc0534c2694279fc6e46d38f21a3f6ed3
    Private Spend Key    : dd62d51183f6208cf4d1b9af523f2c80bf534c2694279fc6e46d38f21a3f6e03
    Private View Key     : 7838567e050aa2dc3964bca85c3a42d9cec5b77b3d8f055e2763641fdce53c07
    Public Spend Key     : deb53426c8ea9bc20581d0a9489e5b71df16219008c45e7747db98c42d7cf522
    Public View Key      : 9736ad5236981e2044f0b8ebb3bd790d32f896837d501b83712e3fd920191718
    Monero Address       : 4A4cAKxSbirZTFbkK5LwoYL3hLkVxkT8yLxAz8KCxAT66naEG4pYY9B6Q43zdao1oE3D3mzodbggzNz9t9tGvE8N3jVnu3A
    Electrum Seed Words  : bacon enigma gasp furnished memoir aunt input makeup dodge amended hookup tyrant syringe tinted absorb science cement vacation inexact kiwi inflamed sensible mews motherly memoir

Contrast ./xmr results above from what https://xmr.llcoins.net/addresstests.html yields using e62551cad9fe0f05d7c84cf6a0ef7e8fc0534c2694279fc6e46d38f21a3f6ed3 as the "Hexadecimal Seed".  There are two sets of Electrum seed words that result in the same Monero address. Subtle differences can be easily explained by knowing if the seed is already normalized (i.e., sc_reduce32 is applied) or not.

### 11) Ethereum (ETH) BIP 39/44 Technology [Examples](https://medium.com/@alexberegszaszi/why-do-my-bip32-wallets-disagree-6f3254cc5846#.mwhwon7af):

**Ethereum Hexadecimal m/44'/60'/0'/0/0 Private Key** 
```
% echo "radar blur cabbage chef fix engine embark joy scheme fiction master release" | bx mnemonic-to-seed | bx hd-new -v 76066276 | bx hd-private -d -i 44 | bx hd-private -d -i 60 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec
```
```
radar blur cabbage chef fix engine embark joy scheme fiction master release
ed37b3442b3d550d0fbb6f01f20aac041c245d4911e13452cac7b1676a070eda66771b71c0083b34cc57ca9c327c459a0ec3600dbaf7f238ff27626c8430a806
xprv9s21ZrQH143K2weTjKTSMXUM1qmfYo2iDQGPrzsbirKyf9Qn325C8DtapD8dwUL2PU8ciZ9hYVSL4Q9VkygWBosS8FMuX65QqxZQmBDYSEq
xprv9vTgjZ7XMB6PSvXz5HeF2xw7GgqpjmTgy76jrNkUkZFfWzKAD1GMyxoMhJCKgCH3WKw3yhXSBuP4Gxmwp5V4ZQVv1wSV7ARQPacbLkwNdBp
xprv9w29xFAdfTWFMXugTrP7x1X8c75gYKZFUEhGFqhbGxAwpJnWSo1QZUWPgr2XRKsdsdFPiKKaixbj1gZ2r63NS4EKUkjfii41gWKC5VU8gsh
xprv9zWvV2FbEX7VzS96sZG1dZ7MY2j4iFDB62kfuwU95q22omhL7EpQGutw9GyRa9tic3uRnCVZXMLApeDrKb9qJrrUKZzG5dDX29BZwLaTmGZ
xprvA1Qqm9XD31nDSB9iYUf4YN6Ycg2Yxey9ecZeDt4rsqUfTqjSoxsW65Ds49xftNDuxDaGUwk9ZtL3sUYeRCEHLjuU95shHpmLwbwM1nVxbXf
xprvA2xEQ2iTe9QB22rvf5cbfpUxEBmMdvc7stEFxLhiMXmdLrwLbqugPCHRZiRfEq2puC5vTgwyFneV38hppF8oTf9aoaUv7M8u2XvnACTe6r4
b96e9ccb774cc33213cbcb2c69d3cdae17b0fe4888a1ccd343cbd1a17fd98b18
```

**Ethereum Hexadecimal M/44'/60'/0'/0/0 Public Address:**
```
% echo "radar blur cabbage chef fix engine embark joy scheme fiction master release" | bx mnemonic-to-seed | bx hd-new -v 76066276 | bx hd-private -d -i 44 | bx hd-private -d -i 60 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec | bx ec-to-public -u | sed 's/^..//' | ./kec | sed 's/^........................//'
```
```
radar blur cabbage chef fix engine embark joy scheme fiction master release
ed37b3442b3d550d0fbb6f01f20aac041c245d4911e13452cac7b1676a070eda66771b71c0083b34cc57ca9c327c459a0ec3600dbaf7f238ff27626c8430a806
xprv9s21ZrQH143K2weTjKTSMXUM1qmfYo2iDQGPrzsbirKyf9Qn325C8DtapD8dwUL2PU8ciZ9hYVSL4Q9VkygWBosS8FMuX65QqxZQmBDYSEq
xprv9vTgjZ7XMB6PSvXz5HeF2xw7GgqpjmTgy76jrNkUkZFfWzKAD1GMyxoMhJCKgCH3WKw3yhXSBuP4Gxmwp5V4ZQVv1wSV7ARQPacbLkwNdBp
xprv9w29xFAdfTWFMXugTrP7x1X8c75gYKZFUEhGFqhbGxAwpJnWSo1QZUWPgr2XRKsdsdFPiKKaixbj1gZ2r63NS4EKUkjfii41gWKC5VU8gsh
xprv9zWvV2FbEX7VzS96sZG1dZ7MY2j4iFDB62kfuwU95q22omhL7EpQGutw9GyRa9tic3uRnCVZXMLApeDrKb9qJrrUKZzG5dDX29BZwLaTmGZ
xprvA1Qqm9XD31nDSB9iYUf4YN6Ycg2Yxey9ecZeDt4rsqUfTqjSoxsW65Ds49xftNDuxDaGUwk9ZtL3sUYeRCEHLjuU95shHpmLwbwM1nVxbXf
xprvA2xEQ2iTe9QB22rvf5cbfpUxEBmMdvc7stEFxLhiMXmdLrwLbqugPCHRZiRfEq2puC5vTgwyFneV38hppF8oTf9aoaUv7M8u2XvnACTe6r4
b96e9ccb774cc33213cbcb2c69d3cdae17b0fe4888a1ccd343cbd1a17fd98b18
0405b7d0996e99c4a49e6c3b83288f4740d53662839eab1d97d14660696944b8bbe24fabdd03888410ace3fa4c5a809e398f036f7b99d04f82a012dca95701d103
05b7d0996e99c4a49e6c3b83288f4740d53662839eab1d97d14660696944b8bbe24fabdd03888410ace3fa4c5a809e398f036f7b99d04f82a012dca95701d103
0AB3387A148B3C4B18C333FCAC39B311DCEB2A4B2F5D8461C1CDAF756F4F7AE9
AC39B311DCEB2A4B2F5D8461C1CDAF756F4F7AE9
```

### 12) Open Assets Examples:

**Test Vector Examples:**

**A.** [Coloring of Bitcoin](https://github.com/OpenAssets/open-assets-protocol/blob/master/specification.mediawiki#protocol-overview): **Layering**
```
% bx ec-to-public -u "18E14A7B6A307F426A94F8114701E7C8E774E7F9A47E2C2035DB29A206321725" | bx bitcoin160 | bx base58check-encode -v 0 
```
```
0450863ad64a87ae8a2fe83c1af1a8403cb53f53e486d8511dad8a04887e5b23522cd470243453a299fa9e77237716103abc11a1df38855ed6f2ee187e9c582ba6
010966776006953d5567439e5e39f86a0d273bee
16UwLL9Risc3QfPqBUvKofHmBQ7wMtjvM
``` 

**B.** [Open Assets Address](https://github.com/OpenAssets/open-assets-protocol/blob/master/address-format.mediawiki#example): **version_p2pkh**
```
% bx base58check-encode -v 19 00010966776006953d5567439e5e39f86a0d273bee
```
```
akB4NBW9UuCmHuepksob6yfZs6naHtRCPNy
```
Is equivalent to
```
% bx wrap-encode -v 19 00010966776006953d5567439e5e39f86a0d273bee | bx base58-encode
```
```
1300010966776006953d5567439e5e39f86a0d273bee852783aa
akB4NBW9UuCmHuepksob6yfZs6naHtRCPNy
```

**C.** [Open Assets ID](https://github.com/OpenAssets/open-assets-protocol/blob/master/specification.mediawiki#protocol-overview): **version_p2sh**
```
% bx script-to-address -v 23 "dup hash160 [ 010966776006953D5567439E5E39F86A0D273BEE ] equalverify checksig"
```
```
ALn3aK1fSuG27N96UGYB1kUYUpGKRhBuBC
```
Is equivalent to:
```
% bx script-encode "dup hash160 [ 010966776006953D5567439E5E39F86A0D273BEE ] equalverify checksig" | bx bitcoin160 | bx address-encode -v 23
```
```
76a914010966776006953d5567439e5e39f86a0d273bee88ac
36e0ea8e93eaa0285d641305f4c81e563aa570a2
ALn3aK1fSuG27N96UGYB1kUYUpGKRhBuBC
```