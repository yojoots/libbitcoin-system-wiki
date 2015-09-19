### Application of BIP [32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), [38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki), [39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), [44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki), and 63 ([Stealth Addresses](http://sourceforge.net/p/bitcoin/mailman/message/31813471/)) to Altcoins

Libbitcoin has an established the bitcoin-explorer **(bx)** command line interface that provides substantial BIP 32, 38, 39, and 63 support.  BIP 44 support results from how bx BIP 32 is applied and the application of the table below. This table is not only for BTC, but numerous other altcoins.

**1) Combined BIP 32 and 44 example:** Apply m/44’/5’/0’/0/0 example to create a compressed Dash private key.
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204                                                                     
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM 

% echo 'tprv8iBUTxFHtPMKmrQDN4yjCPWmNBT9ZPZZeSFgxNLnAhmNmsHVmFxENnREcdEQXLVUoE3invSjhTjDsHfCrVtijVvVYbj6XWfH6DmQnXQvQoZ' | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM
```

**2) Combined BIP 32 and 44 example:** Apply m/44’/5’/0’/0/0 to create a compressed Dash public addresses for up to 4 billions addresses much more safely on an online machine!!!
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-public  -i 0         | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76   
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2 <- Don't use the command above on an online computer!

% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 0 | bx hd-to-ec | bx    ec-to-address -v 76
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2  <- Don't be afraid to apply the command above on an online computer (Could be a death knell to PCI-DSS Compliance for eCommerce if cryptocurrencies become more widely adopted)

% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 1 | bx hd-to-ec | bx    ec-to-address -v 76
XpTtgbcURSBfcuo8FZsNFeGrsCSi3jarAi  <- Don't be afraid to apply the command above on an online computer
```

3) **BIP 39 example:** Create master seed in Spanish from a weak English brainwallet seed. (Is altcoin insensitive.)
```
% echo 'very complex gibberish' | bx base16-encode | bx sha512 | bx mnemonic-new -l es
cambio cosmos leche dar imponer enfermo envío equipo tanque liso utopía semilla altar bebé proa caoba maestro bodega equipo escribir droga paso apodo bulto vela molino nave talento militar perder odiar árido signo enfermo rojizo ganso himno clase átomo chupar rienda quitar ciclón banda situar rueda alto asesor
```

4) **BIP 39 example:** Recreate master seed from BIP 39 words. (Is altcoin insensitive.)
```
% echo 'enable load garage hard diagram trim nothing exclude fantasy gold ramp fiber wise ball have hero toddler spy excite glue maze drill else sell' | bx mnemonic-to-seed -p TREZOR
f0e63d191d75d39b5d1d8d1ae8ff1c48e51cacffb6d3881f31715572a59f352d35fa44a7e84f9a69712b206b9e04966a5794470993516e1b363a001fc3917f69
```

The libbitcoin table below is a work-in-progress, but it provided important values for the first two working examples above. Accuracy of portions of this table is questionable (~90% accurate) until vetted by other subject matter experts, but the pattern for how it is applied to altcoins is well understood. This table most definitely complements [SLIP 44] (http://doc.satoshilabs.com/slips/slip-0044.html) referenced within [BIP44] (https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#registered-coin-types)

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
      |              |                    |                 |   https://github.com/OpenAssets/open-assets-protocol/blob/master/specification.mediawiki#protocol-overview ( % echo 'dup hash160 [ 010966776006953D5567439E5E39F86A0D273BEE ] equalverify checksig' | bx script-encode | bx sha256 | bx ripemd160  =>  Yields Open Assets ID: ALn3aK1fSuG27N96UGYB1kUYUpGKRhBuBC )
```

### [Wallet Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Wallet-Commands)

The table above is a "Rosetta Stone" to effectively translate Bitcoin private keys and public addresses to those used by a number of altcoins having strong Bitcoin heritage. It provides important **--version (-v)** base-10 integer values for the following **bitcoin-explorer** commands to create keys and addresses for altcoins:

* **base58check-encode** ( use version/WIF column )
* **ec-to-address**      ( use version/p2pkh column )

The following bitcoin explorer commands are natural candidates to be extended to accommodate **--version** values:

* **ec-to-wif**          ( recommend using version/WIF column )
* **hd-to-address**      ( recommend using p2pkh column )
* **hd-to-wif**          ( recommend using version/WIF column )

### [Key Encryption Commands] (https://github.com/libbitcoin/libbitcoin-explorer/wiki/Key-Encryption-Commands)

The table above also complements [Altchain Encrypted Private Keys](https://github.com/libbitcoin/libbitcoin/wiki/Altchain-Encrypted-Private-Keys) by supporting the following **bitcoin-explorer** "encrypted key" commands to extend **alpha BIP 38 functionality** to altcoins:

* **ec-to-ek**    ( use version/p2pkh column )  *<- Should this ultimately be ( using version/WIF column )?*
* **ek-address**  ( use version/p2pkh column )
* **ek-new**      ( use version/p2pkh column )  *<- Should this ultimately be ( using version/WIF column )?*
* **ek-public**   ( use version/p2pkh column )

### [Stealth Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Stealth-Commands)

The application **--versions** values to **Stealth Commands** for altcoins is a work in progress...

