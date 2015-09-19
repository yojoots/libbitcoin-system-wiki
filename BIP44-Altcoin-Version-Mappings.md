### Application of BIP [32](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki), [38](https://github.com/bitcoin/bips/blob/master/bip-0038.mediawiki), [39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki), [44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki), and 63 ([Stealth Addresses](http://sourceforge.net/p/bitcoin/mailman/message/31813471/)) to Altcoins

Libbitcoin bitcoin-explorer **(bx)** command line interface provides substantial BIP 32, 38, 39, and 63 support.  BIP 44 support results from how bx BIP 32 is applied and the application of the table below. This table applies to BTC and numerous other altcoins.

The table below is a work-in-progress, but provides important values for the first two working examples below the table. Accuracy of portions of this table is questionable (~90% accurate) until vetted by others, but the pattern for how it is applies to altcoins is well understood. This Altcoin Version Mapping Table most definitely extends/complements [SLIP 44] (http://doc.satoshilabs.com/slips/slip-0044.html) referenced within [BIP44] (https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#registered-coin-types)

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

**1) Combined BIP 32 and 44 example:** Apply m/44’/5’/0’/0/0 example to create a compressed Dash private key.
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-private -i 0 | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204                                                                     
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM 

% echo 'tprv8iBUTxFHtPMKmrQDN4yjCPWmNBT9ZPZZeSFgxNLnAhmNmsHVmFxENnREcdEQXLVUoE3invSjhTjDsHfCrVtijVvVYbj6XWfH6DmQnXQvQoZ' | bx hd-private -i 0 | bx hd-to-ec | sed 's/$/01/' | bx base58check-encode -v 204
XH2Yndjv6Ks3XEHGaSMDhUMTAMZTTWv5nEN958Y7VMyQXBCJVQmM
```

**2) Combined BIP 32 and 44 example:** Apply m/44’/5’/0’/0/0 to create a compressed Dash public addresses for up to 4 billions addresses much more safely on an online machine!!!
```
% echo 'very complex gibberish' | bx base16-encode | bx sha256 | bx hd-new | bx hd-private -d -i 44 | bx hd-private -d -i 5 | bx hd-private -d -i 0 | bx hd-public  -i 0 | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76   
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2 <- Be very afraid to use the seed-driven command sequence above on an online computer!

% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 0 | bx hd-to-ec | bx ec-to-address -v 76
Xb9HJy46M9u3SLAWVitS4eV6gEMuVFfZX2  <- Don't be afraid to apply the chain code driven command sequence above on an online computer (Could be a death knell to PCI-DSS Compliance for eCommerce if cryptocurrencies become more widely adopted)

% echo 'tpubDEsWcNHY2m2zfKS1FieKboAswCy5iikUDjrUEtP5ayZmcMYGPempZH36nn9MTMpRqcXowhdDTGwsPu5pcGJ95g6kVKTN7ynmc5pKjjURSqz' | bx hd-public  -i 1 | bx hd-to-ec | bx ec-to-address -v 76
XpTtgbcURSBfcuo8FZsNFeGrsCSi3jarAi  <- Don't be afraid to apply the chain code driven command sequence above on an online computer
```

**3) BIP 39 example:** Create master seed in Spanish from a weak English brainwallet seed. (Is altcoin insensitive.)
```
% echo 'very complex gibberish' | bx base16-encode | bx sha512 | bx mnemonic-new -l es
cambio cosmos leche dar imponer enfermo envío equipo tanque liso utopía semilla altar bebé proa caoba maestro bodega equipo escribir droga paso apodo bulto vela molino nave talento militar perder odiar árido signo enfermo rojizo ganso himno clase átomo chupar rienda quitar ciclón banda situar rueda alto asesor
```

**4) BIP 39 example:** Recreate master seed from BIP 39 words. (Is altcoin insensitive.)
```
% echo 'enable load garage hard diagram trim nothing exclude fantasy gold ramp fiber wise ball have hero toddler spy excite glue maze drill else sell' | bx mnemonic-to-seed -p TREZOR
f0e63d191d75d39b5d1d8d1ae8ff1c48e51cacffb6d3881f31715572a59f352d35fa44a7e84f9a69712b206b9e04966a5794470993516e1b363a001fc3917f69
```

The following bitcoin explorer commands are natural candidates to be extended to accommodate **--version** values:

* **ec-to-wif**          ( recommend using version/WIF column )
* **hd-to-address**      ( recommend using p2pkh column )
* **hd-to-wif**          ( recommend using version/WIF column )

### [Key Encryption Commands] (https://github.com/libbitcoin/libbitcoin-explorer/wiki/Key-Encryption-Commands)

The table above also complements [Altchain Encrypted Private Keys](https://github.com/libbitcoin/libbitcoin/wiki/Altchain-Encrypted-Private-Keys) by supporting the following **bitcoin-explorer** "encrypted key" commands to extend **alpha BIP 38 functionality** to altcoins:

* **ec-to-ek**    ( [use version/p2pkh column](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ec-to-ek#example-6) )  *<- Should current linked example be ( using version/WIF column )?*
* **ek-address**  ( use version/p2pkh column )
* **ek-new**      ( [use version/p2pkh column](https://github.com/libbitcoin/libbitcoin-explorer/wiki/bx-ek-new#example-6) )  *<- Should current linked example be ( using version/WIF column )?*
* **ek-public**   ( use version/p2pkh column )

**5) Extended AES256Encrypt and AES256Decrypt BIP 38 example:** For a Dash base16-encoded 256-bit secret elliptic curve key.

```
% bx ec-to-ek -v 204 'Hello it is me' f9a8f6d4a24b99d4944ee3db83c85383e9c13e85cb50ad60a9e1a96e02f6d269
5XCsGSbMhW6zisvPx7LUKHPUGTi21kdSVwc6HNM1Zurg9ENPiUVtzBZDho

% bx ek-to-ec 'Hello it is me' 5XCsGSbMhW6zisvPx7LUKHPUGTi21kdSVwc6HNM1Zurg9ENPiUVtzBZDho
f9a8f6d4a24b99d4944ee3db83c85383e9c13e85cb50ad60a9e1a96e02f6d269
```
**6) Extended "EC Multiply Mode" BIP 38 example:** For Dash with an initial secret of 'knock knock', seed, salt, lot number of 0, and sequence number of 0. *Please note the information below must be correlated with security [recommendations](https://github.com/libbitcoin/libbitcoin/wiki/BIP38-Security-Considerations#recommendations) to arrive at a good processes for minting coins or engraving notes.*

```
% echo 'Not so random seed' | bx base16-encode | bx sha256
565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857 <- Seed

% echo 'a little salt & pepper' | bx base16-encode | bx sha256
e51549349dd7b98ff30281211fe281247c32922d259fc12b0abf7b2110114d03 <- First 8 hex digits are used as salt.

% bx token-new -l 0 -s 0 'knock knock' e5154934
passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg <- Intermediate code created by future coin/note owner to outsource work to a minter/engraver. Both this information and the seed are released only to the minter/engraver.

% bx ek-new -v 204 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
5XTqTrYMNKoHHcfqafEX5nFZTLnNwXF5Zf6fjYP8cDqNDwzPxendxaCMGw <- Performed by the minter/engraver to know the BIP 38 encrypted private key to be publicly labelled on the coin/note. 

% bx ek-to-ec 'knock knock' 5XTqTrYMNKoHHcfqafEX5nFZTLnNwXF5Zf6fjYP8cDqNDwzPxendxaCMGw
cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23 <- EC synthesized private key; test point #1 (TP1)

% echo 'cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23' | bx ec-to-public
035d37339d296b1a7ea8c7f04cf33eb0e8fd547df58d60259c9e4d9404795cd7f1 <- EC synthesized public key; (TP2)

% echo 'cb77527dfc18a491e79fa34de3b8ce0b3e1f2ce8db2e1fcd69139010505adb23' | bx ec-to-public  | bx ec-to-address -v 76
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu  <- Dash address where funds are to be deposited; (TP3) 

% bx ek-public -v 76 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
cfrm3CdFNyDReVUXn2weQYL4Q3sGsRyFYSNBbrK5qfpFyCXCNKPPJicRxuxmLiN3ZtjVafCLZuc <- Created by the minter/engraver. To avoid being classified as "money transmitter" minter/engraver must not send/share this information with the coin/note owner until after the coin/note is sent by registered mail, preferably delivered. However, there are no explicit counter measures preventing entrapment by a "devious" coin/note owner by the BIP 38 protocol!!!

% bx ek-public-to-ec 'knock knock' cfrm3CdFNyDReVUXn2weQYL4Q3sGsRyFYSNBbrK5qfpFyCXCNKPPJicRxuxmLiN3ZtjVafCLZuc 
035d37339d296b1a7ea8c7f04cf33eb0e8fd547df58d60259c9e4d9404795cd7f1 <- matches TP2

% bx ek-public-to-address 'knock knock' cfrm3CdFNyDReVUXn2weQYL4Q3sGsRyFYSNBbrK5qfpFyCXCNKPPJicRxuxmLiN3ZtjVafCLZuc
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu <- Performed by coin/note owner after receiving the confirmation code from the minter/engraver.  If public address doesn't match the results of the next command, coin/note owner should not "load" the coin with the denomination printed on the coin. (matches TP3)

% bx ek-address -v 76 passphrasedsP52SrHdFSR4Fb55dvDiXnxnuyZUFCYheSYrPVGiMUCVnEhCb4UU3Nsbs2HCg 565bdb03ade36264adc00600952a865fc4bdc61d81be7d9be6ee0c7c06809857
Xc3cYycMHt9vtBjMcUJshBH34QqfZnbEyu <- Performed by coin/note owner to authenticate the Dash coin address where funds are to be deposited. If there is a match, a deposit won't either be lost or burned. (matches TP3)
```


### [Stealth Commands](https://github.com/libbitcoin/libbitcoin-explorer/wiki/Stealth-Commands)

The application **--versions** values to **Stealth Commands** for altcoins is a work in progress...

