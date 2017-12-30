In [Social Network Principle](Social-Network-Principle) it is shown that Bitcoin is a network of [human](Glossary#person) relationships. This can be modeled as a [directed graph](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics)#Directed_graph) where each vertex represents a [merchant](Glossary#merchant) and each edge represents a [trade](Glossary#trade) for bitcoin. Edges indicate the direction of movement of [coin](Glossary#coin) and are quantified in the number of [units](Glossary#unit) traded. All [owners](Glossary#owner) are presumed to have been merchants at the time of coin receipt, including as [miners](Glossary#miner) (selling [confirmations](Glossary#confirmation)) and as recipients of charity (selling [goodwill](https://en.wikipedia.org/wiki/Goodwill_(accounting))).

If a person is not personally accepting coin, or does not personally [validate](Glossary#validation) coin accepted, the person cannot reject invalid coin. The person is entrusting this task to a [central](Glossary#centralization) authority. Similarly, when a person [delegates](Glossary#delegation) coin to another party, the person no longer owns the coin. In both cases the person controls only a promise to trade back the coin and therefore does not [contribute to security](Risk-Sharing-Principle). All people utilizing the same delegate are reduced to just one vertex that represents the delegate.

For any period of time, [economic](Glossary#economy) security is a function of the number of merchants and the similarity of amounts traded. The strongest economy would be all people in the world trading for the same number of units in the period, an ideal which can be called a "distributed" (or fully-decentralized) economy. The weakest would be one delegate accepting all units traded in the period, which would be a "centralized" economy.

More specifically, the system is most decentralized which has the greatest number of vertices (merchants) with the lowest [coefficient of variation ("variation")](https://en.wikipedia.org/wiki/Coefficient_of_variation) in the sum of incoming edges (receipts). Defining the *distribution* function as the inverse of variation we obtain:
```
economic-decentralization = merchants * distribution(receipts)
```
Similar to economic security, confirmation security can be modeled as an [edgeless graph](https://en.wikipedia.org/wiki/Null_graph). Each [miner](Glossary#miner) is represented by one vertex on the graph. A [grinder](Glossary#grinder) is not a miner as the grinder has no decision-making ability, only the miner is represented. The total [hash power](Glossary#hash-power) employed by a miner is the weight of the vertex. The strongest censorship resistance is every person in the world mining with equal hash power.

The systemic mining [threat](Glossary#state) is motivated by [censorship](Glossary#censorship), not [double-spending](Glossary#double-spend). Total [hash rate](Glossary#hash-rate) provides security against such attacks, but [pooling](Glossary#pooling) of hash rate works against it. As mining collects into [pools](Glossary#pooling) it becomes cheaper to [co-opt](Glossary#co-option) than to compete against it.

For any period of time, confirmation security is a function of the number of miners and the similarity of hash power they directed. The strongest censorship resistance would be all people in the world mining at the same hash power in the period, an ideal which can be called "distributed" (or fully-decentralized) confirmation. The weakest would be one miner with 100% of hash power, which would be "centralized" confirmation.

More specifically, the system is most decentralized which has the greatest number of vertices (miners) with the highest distribution in weights (hash power):
```
confirmation-decentralization = miners / distribution(hash-power)
```
While people could decide to trade and/or mine independently in the future, they do not [contribute to security](Risk=Sharing-Principle) until after they actually do so. The distinction is analogous to being armed vs. having the ability to become armed. As shown in [Cockroach Fallacy](Cockroach-Fallacy), the latter matters not when you are getting robbed. The model represents security as it actually exits in the period.

As show in in [Public-Data-Principle](Public-Data-Principle), anonymity is a tool that aids in defending one's ability to trade and/or mine. As such the level of decentralization can never be measured. The model is a conceptual aid. Additionally, as shown in [Balance of Power Fallacy](Balance-of-Power-Fallacy), the the security afforded by each of the two sub-models is complimentary and independent of the other.

Decentralization alone is not security. **Security is the product of activity, distribution of that activity and the fraction of participating humanity.**
```
security = activity * distribution * participation
```
Given that there is no limit to humanity, trade or computation, the level of security in each axis is unbounded. A minimum level of zero in each is achieved with either no participation or no activity.

CV is the ratio of [standard deviation (sd)](https://en.wikipedia.org/wiki/Standard_deviation) to the [arithmetic mean](https://en.wikipedia.org/wiki/Arithmetic_mean)

Economic security can be defined as:
```
economic-security = receipts * economic-decentralization / humanity
economic-security = receipts * [merchants * distribution(receipts)] / humanity
economic-security = receipts * distribution(receipts) * [merchants / humanity]
economic-security = receipts / variation(receipts) * [merchants / humanity]
```

Confirmation security can be defined as:
```
confirmation-security = hash-power * confirmation-decentralization / humanity
confirmation-security = hash-power * [miners * distribution(hash-power)] / humanity
confirmation-security = hash-power * distribution(hash-power) * [miners / humanity]
confirmation-security = hash-power / variation(hash-power) * [miners / humanity]
```

These relations do not say anything about the absolute effectiveness represented by any value, or the relative effectiveness of any two values except that a greater value represents a greater effectiveness. This is not due to a deficiency in the method. The factors include people, specifically the effectiveness of their individual abilities to resist (and their perception of value in the money). All who validate or mine offer some level of resistance, but there is no implied continuity. We refer to a "level" of security, not an "amount" of security.