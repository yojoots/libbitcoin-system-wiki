## Integrating BIP 32, 38, 39, 44, and 63 Technologies with Altcoins   

The libbitcoin table below is a work-in-progress... Accuracy of portions of this table is questionable (~90% accurate) until vetted by other subject matter experts, but the pattern for how it is applied to altcoins is well understood. This table most definitely complements [SLIP 44] (http://doc.satoshilabs.com/slips/slip-0044.html) referenced within [BIP44] (https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#registered-coin-types)

## BIP44 Altcoin Version Mapping Table
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
      |              |                    |                 |   https://github.com/OpenAssets/open-assets-protocol/blob/master/specification.mediawiki#protocol-overview ( % echo 'dup hash160 [ 010966776006953D5567439E5E39F86A0D273BEE ] equalverify checksig' | bx script-encode | bx sha256 | bx ripemd160  =>  Yields Open Assets ID: ALn3aK1fSuG27N96UGYB1kUYUpGKRhBuBC )
```

## [Wallet Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Wallet-Commands)

The table above is a "Rosetta Stone" to effectively translate Bitcoin private keys and public addresses to those used by a number of altcoins having strong Bitcoin heritage. It provides important **--version (-v)** base-10 integer values for the following **bitcoin-explorer** commands to create keys and addresses for altcoins:

* **base58check-encode** ( use version/WIF column )
* **ec-to-address**      ( use version/p2pkh column )

The following bitcoin explorer commands are natural candidates to be extended to accommodate **--version** values:

* **ec-to-wif**          ( recommend using version/WIF column )
* **hd-to-address**      ( recommend using p2pkh column )
* **hd-to-wif**          ( recommend using version/WIF column )

## [Key Encryption Commands] (https://github.com/libbitcoin/libbitcoin-explorer/wiki/Key-Encryption-Commands)

The table above also complements [Altchain Encrypted Private Keys](https://github.com/libbitcoin/libbitcoin/wiki/Altchain-Encrypted-Private-Keys) by supporting the following **bitcoin-explorer** "encrypted key" commands to extend **alpha BIP 38 functionality** to altcoins:

* **ec-to-ek**    ( use version/p2pkh column )  <- Should this ultimately be ( using version/WIF column )?
* **ek-address**  ( use version/p2pkh column )
* **ek-new**      ( use version/p2pkh column )  <- Should this ultimately be ( using version/WIF column )?
* **ek-public**   ( use version/p2pkh column )

## [Stealth Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Stealth-Commands)

The application **--versions** values to **Stealth Commands** is a work in progress...

