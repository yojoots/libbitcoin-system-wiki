It follows from the [risk sharing principle](Risk-Sharing-Principle) that system security depends upon covert [mining](Glossary#mine) and [trade](Glossary#trade). A [coin](Glossary#coin) exists as a [mutually-beneficial](Balance-of-Power-Fallacy) [market](Glossary#market) between [miners](Glossary#miner) and [merchants](Glossary#merchant) for the [confirmation](Glossary#confirmation) of [transactions](Glossary#transaction) within [blocks](Glossary#block) in exchange for [fees](Glossary#fee).

The necessarily covert activities are listed by role:

**Miner**
1. obtain blocks [to build upon]
2. obtain unconfirmed transactions [to earn fees from]
3. create and distribute blocks [to cause others to build upon]
4. receive payment for confirmations [to finance operations]

**Merchant**
1. obtain blocks [to validate customer payment]
2. obtain unconfirmed transactions (optional) [to anticipate payments and fees]
3. create and distribute transactions [to obtain customer payment]
4. make payment for confirmations [to compensate confirmation]

If blocks cannot be obtained anonymously the system is insecure. The inability to obtain the [strongest](Glossary#strong) blocks available to other [people](Glossary#person) is a network [partition](Glossary#partition) that implies localized insecurity. However neither anonymity, nor its opposite [identity](Glossary#identity), can ever ensure one sees the strongest [branch](Glossary#branch) at any given time. In other words any attempt to mitigate partitioning with the introduction of identity is a [false choice](https://en.wikipedia.org/wiki/False_dilemma).

It is not essential that all miners or merchants see all transactions at any given time. However broad visibility is preferable as it produces the most robust competition for fees and best leading information. In other words, a market where every participant sees all of the transactions all of the time is a [perfect market](https://en.wikipedia.org/wiki/Perfect_competition).

Creation of blocks and transactions never exposes identity, however public distribution of either is the primary source of [taint](Glossary#taint). To the extent that miners openly self-identify, they are doing so in a [low-threat environment](Threat-Level-Paradox).