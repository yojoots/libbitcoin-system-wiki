The concept of a pure bank can be useful in demonstrating [lending](Glossary#lend) behavior generally.

A pure bank provides only the following services:

* borrows money (debt from creditors)
* lends money (credit from debtors)
* hoards money (reserve)

The material differences from a real bank are:

* no state intervention (free bank)
* uniform interest (efficient market)
* no cost of operation (efficient operations)

The bank is owned by its creditors in proportion to their credit, as is the case with any company. There are existing major banks that are owned by their account-holders, such as [USAA](https://www.usaa.com) and [Vanguard](https://investor.vanguard.com), so this is not a distinction from a real bank. Neither a pure bank nor a real bank has "own capital" to lend, as all capital is borrowed from investors in one form or another. The objective of creditors is to maximize their rate of return. The objective of debtors is to minimize their [interest](Glossary#interest) expense.

Creditor accounts are [money substitutes](https://wiki.mises.org/wiki/Money_substitutes). This aspect distinguishes the bank from an investment fund. The money substitute may be either a [demand deposit](https://en.wikipedia.org/wiki/Demand_deposit) or a [money market](https://en.wikipedia.org/wiki/Money_market_fund). The distinction is in the allocation of insufficient reserve (negative rate of return), with the former being "[first come, first served](https://en.wikipedia.org/wiki/Bank_run)" and the latter "[breaking the buck](https://en.wikipedia.org/wiki/Money_market_fund#Breaking_the_buck)".

The lack of [state](Glossary#state) intervention is the common concept of [free banking](https://en.wikipedia.org/wiki/Free_banking), where there is no [statutory control](https://en.wikipedia.org/wiki/Federal_Reserve), no state [insurance](https://www.fdic.gov), no [discount capital](https://en.wikipedia.org/wiki/Discount_window), and no [seigniorage](https://en.wikipedia.org/wiki/Seigniorage). The bank uses commodity [money](Money-Taxonomy) unless otherwise specified, which simplifies calculations by [eliminating](Inflation-Principle) the need to offset [price inflation](https://en.wikipedia.org/wiki/Inflation) or [price deflation](https://en.wikipedia.org/wiki/Deflation) with the [Fisher Equation](https://en.wikipedia.org/wiki/Fisher_equation).

Perfect operational efficiency differs from a real bank only in the rate of return, as nothing is consumed in operations. A perfectly [efficient market](https://en.wikipedia.org/wiki/Efficient-market_hypothesis) implies uniform interest, and that all earning is a consequence of [time preference](Time-Preference-Fallacy).

[Reserved](Reserve-Definition) capital is the money in which credit and debt are [settled](https://en.wikipedia.org/wiki/Settlement_(finance)) (zero [maturity](https://en.wikipedia.org/wiki/Maturity_(finance))). [Depreciation](Depreciation-Principle) is the [opportunity cost](https://en.wikipedia.org/wiki/Opportunity_cost) of it not being loaned, also known as "cash drag". Interest relations assume a single [compounding period](https://en.wikipedia.org/wiki/Compound_interest) with the rate of interest over that period. Given the definition of a pure bank, the following relations are absolute.
```
reserved         = borrowed - loaned
depreciation     = interest-rate * reserved
nominal-interest = interest-rate * loaned
return           = nominal-interest
```
For the pure bank, the [reserve fraction](Fractional-Reserve-Fallacy) determines [reserve ratio](https://en.wikipedia.org/wiki/Reserve_requirement), [capital ratio](https://en.wikipedia.org/wiki/Capital_requirement), [debt ratio](https://en.wikipedia.org/wiki/Debt_ratio), [savings ratio](https://en.wikipedia.org/wiki/Golden_Rule_savings_rate) and [return ratio](https://en.wikipedia.org/wiki/Rate_of_return).
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
#### Debt Ratio
```
debt-ratio = borrowed / reserved
debt-ratio = borrowed / (borrowed - loaned)
```
#### Savings Ratio
```
savings-ratio = loaned / reserved
savings-ratio = loaned / (borrowed - loaned)
```
#### Return Ratio
Creditor rate of return is additionally a function of the nominal interest rate. The creditor's rate of return is less than the debtor's nominal interest rate due to cash drag, the necessary cost of demand withdrawal. To reduce this cost, time constraints are typically included in [real bank contracts](https://www.chase.com/content/dam/chasecom/en/checking/documents/deposit_account_agreement.pdf). For example, by law any withdrawal from an interest-bearing U.S. bank account can be delayed for seven days. The creditor can only eliminate cash drag by holding the debt with no settlement assurances.
```
return-ratio = interest-ratio * loaned / borrowed
```
The savings ratio [is the interest ratio](Savings-Relation) in the case of uniform interest.
```
savings-ratio = loaned / reserved
```
Substituting savings ratio and reducing obtains a return ratio also in borrowed and loaned capital.
```
return-ratio = (loaned / reserved) - (loaned / borrowed)
```