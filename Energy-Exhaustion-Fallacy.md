There is a theory that [proof of work](Glossary#proof) (PoW) may exhaust all energy available to people. PoW converts energy into a [monotonically increasing](https://en.wikipedia.org/wiki/Monotonic_function) [double-spend](Glossary#double-spend) barrier for any given [transaction](Glossary#transaction). This is comparable to the energy expended in securing any money against counterfeit (by its own issuer or otherwise).

The purpose of any security measure is to create a cost necessary to overcome the measure; i.e. a financial barrier. Bitcoin creates its double-spend barrier by compelling the [attacker](Glossary#attack) to replace the [branch](Glossary#branch) of the targeted transaction with one of probabilistically greater [work](Glossary#work). Interestingly, such a replacement raises the barrier to subsequent attackers. The amount of energy expended is not independently important. The erected barrier is simply the attacker's necessary financial burden.

For a given [block](Glossary#block) the [reward](Glossary#reward) [value](Glossary#attack) (V) is the product of unit [hash](Glossary#hash) cost (C), [hash rate](Glossary#hash-rate) (H), and period (T).
```
V = C * H * T
```
The [adjustment](Glossary#adjustment) varies [hash rate](Glossary#hash-rate) to maintain a constant period for a given cost and reward.
```
T = V / (C * H)
```
A constant period implies that hash rate is inversely proportional to cost for a given reward.
```
H ~ V / C
```
In other words, for a given level of security (reward value), as energy [price](Glossary#price) increases its consumption decreases. For a given level of demand (security), as supply of energy is reduced the price for any given amount of it increases. Therefore, given the inverse relationship between hash rate and energy cost, energy cannot be exhausted by Bitcoin. The theory is therefore invalid.