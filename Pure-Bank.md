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

The lack of [state](Glossary#state) intervention is the common concept of [free banking](https://en.wikipedia.org/wiki/Free_banking), where there is no [statutory control](https://en.wikipedia.org/wiki/Federal_Reserve), state [insurance](https://www.fdic.gov), [discount capital](https://en.wikipedia.org/wiki/Discount_window), or [seigniorage](https://en.wikipedia.org/wiki/Seigniorage). The bank uses commodity [money](Money-Taxonomy) unless otherwise specified, which simplifies calculations by [eliminating](Inflation-Principle) the need to offset [price inflation](https://en.wikipedia.org/wiki/Inflation) or [price deflation](https://en.wikipedia.org/wiki/Deflation) with the [Fisher Equation](https://en.wikipedia.org/wiki/Fisher_equation).

Perfect operational efficiency differs from a real bank only in the rate of return, as nothing is consumed in operations. A perfectly [efficient market](https://en.wikipedia.org/wiki/Efficient-market_hypothesis) implies uniform interest, and that all earning is a consequence of [time preference](Time-Preference-Fallacy). Uniform interest is ultimately an operational efficiency, as rate [arbitrage](https://en.m.wikipedia.org/wiki/Arbitrage) incurs an expense.

[Reserved](Reserve-Definition) capital is the money in which credit and debt are [settled](https://en.wikipedia.org/wiki/Settlement_(finance)) (zero [maturity](https://en.wikipedia.org/wiki/Maturity_(finance))). [Depreciation](Depreciation-Principle) is the [opportunity cost](https://en.wikipedia.org/wiki/Opportunity_cost) of it not being loaned, also known as "cash drag". Interest relations assume a single [compounding period](https://en.wikipedia.org/wiki/Compound_interest) with the rate of interest over that period. This presentation simplification is inconsequential to implied relations.

Given the preceding definition of a pure bank, the following relations are absolute, where expense ratio is 1 for the pure bank.
```
reserved     = borrowed - loaned
depreciation = interest-rate * reserved
interest     = interest-rate * loaned
return       = expense-ratio * interest
```
For the pure bank, the [reserve ratio](https://en.wikipedia.org/wiki/Reserve_requirement) determines [capital ratio](https://en.wikipedia.org/wiki/Capital_requirement), [debt ratio](https://en.wikipedia.org/wiki/Debt_ratio), [savings ratio](https://en.wikipedia.org/wiki/Golden_Rule_savings_rate) and [return ratio](https://en.wikipedia.org/wiki/Rate_of_return). The remaining relation, between all three factors, is the bank’s [balance sheet](https://en.m.wikipedia.org/wiki/Balance_sheet).
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
Creditor rate of return is additionally a function of the interest rate. The creditor's rate of return is less than the debtor's interest rate due to cash drag, the necessary expense of demand withdrawal. To reduce this expense, time constraints are typically included in [real bank contracts](https://www.chase.com/content/dam/chasecom/en/checking/documents/deposit_account_agreement.pdf). For example, by law any withdrawal from an interest-bearing U.S. bank account can be delayed for seven days. The creditor can only eliminate cash drag by holding the debt in an investment fund (i.e without settlement assurances) as opposed to a bank.
```
return-ratio = interest-ratio * loaned / borrowed
```
As shown in [Savings Relation](Savings-Relation) the savings ratio is the interest ratio in the case of uniform interest.
```
savings-ratio = loaned / reserved
```
Substituting savings ratio and reducing obtains a return ratio also in borrowed and loaned capital.
```
return-ratio = (loaned / reserved) - (loaned / borrowed)
```
The pure bank differs from the free bank only by the absence of operational expense, which directly reduces rate of return.
```
free-bank-return-ratio = return-ratio * expense-ratio
```
The real bank differs from the free bank only by the presence of tax, inclusive of regulatory expense.
```
real-return-ratio = free-bank-return-ratio * tax-expense-ratio
```
The central (state) bank differs from the real bank only by the presence of taxpayer subsidy, inclusive of discounted borrowing.
```
central-return-ratio = real-bank-return-ratio * subsidy-income-ratio
```
Where tax includes seigniorage of the bank money, the Fisher Equation must be applied above to translate the interest rate from a nominal rate to a real rate. No other change is implied other than tax, which is accounted for by the real bank above. This tax is generally the source of subsidy, which is accounted for by the central bank above.