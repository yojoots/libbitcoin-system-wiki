There is a theory that the [mining](Glossary#mine) of empty [blocks](Glossary#block) is an [attack](Glossary#block). The theory does not require that the blocks are mined on a [weak branch](Glossary#weak) in an attempt to enable [double-spending](Glossary#double-spend). It also does not specify what [person](Glossary#person) is attacked.

Consider the following:

* Empty block mining is entirely consistent with [consensus rules](Glossary#consensus-rules) and cannot be reasonably prevented by a new [rule](Glossary#rule).

* The term "attack" implies theft. The [Bitcoin whitepaper](https://bitcoin.org/bitcoin.pdf), for example, uses the term only to describe double-spend attempts.

* A [reward](Glossary#reward) consists of [fees](Glossary#fee) for [transactions](Glossary#transaction) and a [subsidy](Glossary#subsidy) for the block. The miner forgoes transaction fees by not including transactions and is not rewarded for them.

* The miner's [hash power](Glossary#hash-power) contributes proportionally to the security of the network. The subsidy is compensation for that security during the [inflationary](Glossary#inflation) phase. The purpose of inflation is to rationally distribute the [coin](Glossary#coin). The rational distribution is specifically in exchange for hash power, not for transaction inclusion.

For each of these reasons independently the theory is invalid. However it is worth exploring the source of the fallacy. Because mining is a [zero sum game](Zero-Sum-Property), there may be an assumption that mining an empty block somehow takes away the opportunity for blocks to be included. This assumption is incorrect.