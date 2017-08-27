There is a theory that the [mining](Glossary#mine) of empty [blocks](Glossary#block) is an [attack](Glossary#attack). The theory does not require that the blocks are mined on a [weak branch](Glossary#weak) in an attempt to enable [double-spending](Glossary#double-spend). It also does not specify what [person](Glossary#person) is attacked.

Consider the following:

* The term "attack" implies theft. The [Bitcoin whitepaper](https://bitcoin.org/bitcoin.pdf), for example, uses the term only to describe double-spend attempts.

* A [reward](Glossary#reward) consists of [fees](Glossary#fee) for [transactions](Glossary#transaction) and a [subsidy](Glossary#subsidy) for the block. The [miner](Glossary#miner) who forgoes transaction fees by not including transactions is not rewarded for them.

* The miner's [hash power](Glossary#hash-power) contributes proportionally to the security of the network. The subsidy is compensation for that security during the [inflationary](Glossary#inflation) phase. The purpose of inflation is to rationally distribute the [coin](Glossary#coin). The rational distribution is specifically in [exchange](Glossary#exchange) for hash power, not for transaction inclusion.

* Transaction [confirmation](Glossary#confirmation) is not assured. Fees are the *incentive* for confirmation. Lack of confirmation objectively implies insufficient fee.

* Empty block mining is entirely consistent with [consensus rules](Glossary#consensus-rules) and cannot be reasonably prevented by a new [rule](Glossary#rule).

For these reasons the theory is invalid. However it is worth exploring the source of the fallacy. Because of the [Zero Sum Property](Zero-Sum-Property), there may be an assumption that mining an empty block "unfairly" takes away the opportunity for transactions to be confirmed.

Other miners retain the ability to confirm transactions in proportion to their hash power. If 10% of the hash power mines empty blocks, then confirmations will take 10% longer on average. However if a miner removes his/her 10% of the total hash power, confirmations will also take 10% longer on average, until the next difficulty [adjustment](Glossary#adjustment). Yet removing one's hash power is generally not considered an attack.

A miner commits capital to mining, producing hash power. Setting aside the [effects of pooling](Pooling-Pressure-Risk), the miner is subsidized in proportion to hash power produced. Without this hash power other miners would produce the same average number of blocks at proportionally lower [difficulty](Glossary#difficulty). In other words, *actually* attacking [owners](Glossary#owner) would be proportionally cheaper. So despite not being rewarded for including transactions, the miner is securing previously-confirmed transactions.

Given that the [marginal cost](https://en.wikipedia.org/wiki/Marginal_cost) of including a transaction is necessarily below average fee levels, the empty block miner is suffering an opportunity cost. This amounts to the miner subsidizing the security of the [chain](Glossary#chain). While this seems economically irrational in the limited context of the coin, it can be rational due to the offsetting opportunity cost for waiting on a new [candidate](Glossary#candidate) following an [announcement](Glossary#announcement). Nevertheless, mining is inherently subject to financial pressures outside of the coin.

While a given miner may consider it advantageous to mine empty blocks, it is within every other person's [power](Glossary#power) to do otherwise. It is the [exercise of this opportunity](Risk-Sharing-Principle) that secures the coin, even against *actual* attacks. The shaming of those acting on self-interest is ineffective and counterproductive. To the extent that it appears effective in the short term, it only reduces security by shoring up [pooling](Glossary#pooling).