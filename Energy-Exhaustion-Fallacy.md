There is a theory that [proof of work](Glossary#proof) (PoW) may consume all energy available to people. PoW converts energy into a monotonically increasing double-spend difficulty for any given transaction. This is comparable to the energy expended in securing any money against counterfeit by its own issuer or otherwise.

The purpose of any security measure is to create a cost necessary to overcome the measure; i.e. a financial barrier. Bitcoin creates its double-spend barrier by compelling the attacker to replace the branch of the targeted transaction with one of provably greater work. Interestingly, such a replacement raises the barrier to subsequent attackers. The amount of energy expended is not independently important. The erected barrier is simply the attacker's necessary financial burden.

Reward (R) is the product of unit hash cost (C), hash rate (H), and time period (T).
```
R = C * H * T
```
The difficulty adjustment varies required hash rate to maintain a constant period for a given cost and reward.
```
T = R / (C * H)
```
A constant period implies that the product of cost and hash rate varies directly with reward.
```
C * H ~ R
```
Or that hash rate is inversely proportional to cost.
```
H ~ R / C
```
So as energy cost increases, its consumption decreases for a given level of security.

For a given level of demand (security), as supply of energy is reduced the price for any given amount of it increases. Therefore, given the inverse relationship between hash rate and energy cost, energy cannot be fully consumed by Bitcoin. The theory is therefore invalid.