The concept of a pure bank can be useful in demonstrating [lending](Glossary#loan) behavior generally.

A pure bank provides only the following services:

* borrows money (debt from creditors)
* lends money (credit from debtors)
* hoards money (reserve)

The material differences from a real bank are:

* no state intervention (free bank)
* uniform interest (efficient market)
* no cost of operation (efficient operations)

The bank is owned by its creditors in proportion to their credit, as is the case with any company. There are existing major banks that are owned by their account-holders, such as [USAA](https://www.usaa.com) and [Vanguard](https://investor.vanguard.com), so this is not a distinction from a real bank. The objective of creditors (owners) is to maximize their income (bank interest paid). The objective of debtors is to minimize their cost (bank interest earned). 


Creditor accounts are [money substitutes](https://wiki.mises.org/wiki/Money_substitutes). The money substitute may be either a [demand deposit](https://en.wikipedia.org/wiki/Demand_deposit) or a [money market fund](https://en.wikipedia.org/wiki/Money_market_fund). The distinction is in the allocation of insufficient reserve, with the former being "[first come, first served](https://en.wikipedia.org/wiki/Bank_run)" and the latter "[breaking the buck](https://en.wikipedia.org/wiki/Money_market_fund#Breaking_the_buck)".

The lack of [state](Glossary#state) intervention is the common concept of [free banking](https://en.wikipedia.org/wiki/Free_banking), where there is no [statutory control](https://en.wikipedia.org/wiki/Federal_Reserve), no state [insurance](https://www.fdic.gov), no [discount capital](https://en.wikipedia.org/wiki/Discount_window), and no [seigniorage](https://en.wikipedia.org/wiki/Seigniorage). The bank uses commodity [money](Money-Taxonomy) unless otherwise specified, which simplifies calculations by [eliminating](Inflation-Principle) the need to offset [price inflation](https://en.wikipedia.org/wiki/Inflation) or [price deflation](https://en.wikipedia.org/wiki/Deflation) using the [Fisher Equation](https://en.wikipedia.org/wiki/Fisher_equation).

Perfect operational efficiency differs from a real bank only in the amount returned to owners, as nothing is consumed in operations. A perfectly [efficient market](https://en.wikipedia.org/wiki/Efficient-market_hypothesis) implies uniform [interest](Glossary#interest), and that all earning is a consequence of [time preference](Time-Preference-Fallacy).

Given the definition of a pure bank, the following relations are absolute. [Reserved](Reserve-Definition) capital is the money in which credit and debt are [settled](https://en.wikipedia.org/wiki/Settlement_(finance)) (zero [maturity](https://en.wikipedia.org/wiki/Maturity_(finance))). [Depreciation](Depreciation-Principle) is the [opportunity cost](https://en.wikipedia.org/wiki/Opportunity_cost) of it not being loaned, also known as "cash drag".
```
reserved        = borrowed - loaned
interest-earned = interest-rate * loaned
depreciation    = interest-rate * reserved
interest-paid   = interest-earned - depreciation
```
For the pure bank, creditor [rate of return](https://en.wikipedia.org/wiki/Rate_of_return), bank [reserve ratio](https://en.wikipedia.org/wiki/Reserve_requirement), and bank [capital ratio](https://en.wikipedia.org/wiki/Capital_requirement) are each functions of the amount borrowed, loaned and the uniform [interest rate](https://en.wikipedia.org/wiki/Interest_rate). Notice that return on borrowed capital is lower than interest due to depreciation of the reserve. This is a consequence of liquidity required to support the money substitute (i.e. demand withdrawal).

#### Rate of Return
```
return-rate = interest-paid / borrowed
return-rate = (interest-earned - depreciation) / borrowed
return-rate = (interest-rate * loaned - interest-rate * reserved) / borrowed
return-rate = (interest-rate * loaned - (interest-rate * (borrowed - loaned))) / borrowed
return-rate = (interest-rate * (loaned - (borrowed - loaned))) / borrowed
return-rate = (interest-rate * (2 * loaned - borrowed)) / borrowed
```
#### Reserve Ratio
```
reserve-ratio = reserved / borrowed
reserve-ratio = (borrowed - loaned) / borrowed
```
#### Capital Ratio
```
capital-ratio = reserved / loaned
capital-ratio = (borrowed - loaned) / loaned
```