The concept of a pure bank can be useful in demonstrating [lending](Glossary#lend) behavior generally.

A pure bank provides only the following services:

* borrows money (debt from creditors)
* lends money (credit from debtors)
* hoards money (reserve)

The material differences from a real bank are:

* no state intervention (free bank)
* no cost of operation (perfectly efficient)

The bank is owned by its creditors in proportion to their credit, as is the case with any company. There are existing major banks that are owned by their account-holders, such as [USAA](https://www.usaa.com) and [Vanguard](https://investor.vanguard.com), so this is not a distinction from a real bank. Neither a pure bank nor a real bank has "own capital" to lend, as all capital is borrowed from investors in one form or another. The objective of creditors is to maximize their rate of return. The objective of debtors is to minimize their [interest](Glossary#interest) expense.

Creditor accounts are [money substitutes](https://wiki.mises.org/wiki/Money_substitutes). This aspect distinguishes the bank from an investment fund. The money substitute may be either a [demand deposit](https://en.wikipedia.org/wiki/Demand_deposit) or a [money market](https://en.wikipedia.org/wiki/Money_market_fund). The distinction is in the allocation of insufficient reserve (negative rate of return), with the former being "[first come, first served](https://en.wikipedia.org/wiki/Bank_run)" and the latter "[breaking the buck](https://en.wikipedia.org/wiki/Money_market_fund#Breaking_the_buck)".

The lack of state intervention is the common concept of [free banking](https://en.wikipedia.org/wiki/Free_banking), where there is no [statutory control](https://en.wikipedia.org/wiki/Federal_Reserve), state [insurance](https://www.fdic.gov), [discount capital](https://en.wikipedia.org/wiki/Discount_window), or [seigniorage](https://en.wikipedia.org/wiki/Seigniorage). The bank uses commodity [money](Money-Taxonomy) unless otherwise specified, which simplifies calculations by [eliminating](Inflation-Principle) the need to offset [price inflation](https://en.wikipedia.org/wiki/Inflation) or [price deflation](https://en.wikipedia.org/wiki/Deflation).

Perfect efficiency differs from a real bank only in the rate of return, as nothing is consumed in operations. All earning is a consequence of [time preference](Time-Preference-Fallacy). Uniform interest is assumed, as rate [arbitrage](https://en.m.wikipedia.org/wiki/Arbitrage) is an expense. [Demurrage](https://en.wikipedia.org/wiki/Demurrage_(currency)) is the expense of storing money. The expense ratio (inclusive of demurrage) is 1 for the pure bank.

[Reserved](Reserve-Definition) capital is the money in which credit and debt are [settled](https://en.wikipedia.org/wiki/Settlement_(finance)) (zero [maturity](https://en.wikipedia.org/wiki/Maturity_(finance))). [Depreciation](Depreciation-Principle) is the [opportunity cost](https://en.wikipedia.org/wiki/Opportunity_cost) of it not being loaned, also known as "cash drag". Interest relations assume a single [compounding period](https://en.wikipedia.org/wiki/Compound_interest) with the rate of interest over that period. This presentation simplification is inconsequential to implied relations.

Given the preceding definition of a pure bank, the following relations are absolute.
```
reserved     = borrowed - loaned
demurrage    = demurrage-rate * reserved
depreciation = interest-rate * reserved
interest     = interest-rate * loaned
return       = expense-ratio * interest
```
For the pure bank, the [reserve ratio](https://en.wikipedia.org/wiki/Reserve_requirement) fully determines [capital ratio](https://en.wikipedia.org/wiki/Capital_requirement), [debt ratio](https://en.wikipedia.org/wiki/Debt_ratio), [savings ratio](https://en.wikipedia.org/wiki/Golden_Rule_savings_rate), [balance sheet](https://en.m.wikipedia.org/wiki/Balance_sheet) and [rate of return](https://en.wikipedia.org/wiki/Rate_of_return).
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
#### Balance Sheet
The pure bank has no liabilities, only shareholder equity.

|bank assets       |shareholder equity |
|------------------|-------------------|
|loaned + reserved |borrowed           |

#### Rate of Return
Creditor rate of return is additionally a function of the interest rate. The creditor's rate of return is less than the debtor's interest rate due to cash drag, the necessary expense of demand withdrawal. To reduce this expense, time constraints are typically included in [real bank contracts](https://www.chase.com/content/dam/chasecom/en/checking/documents/deposit_account_agreement.pdf). For example, by law any withdrawal from an interest-bearing U.S. bank account can be delayed for seven days. The creditor can only eliminate cash drag by holding the debt in an investment fund (i.e without settlement assurances) as opposed to a bank.
```
return-rate = interest-rate * loaned / borrowed
```
As shown in [Savings Relation](Savings-Relation) the capital ratio is the interest rate. The capital ratio includes present goods depreciation, which for money is demurrage. The pure bank demurrage is 1, so this drops out. Substituting capital ratio obtains a rate of return in terms of borrowed and loaned capital.
```
return-rate = (reserved * demurrage-ratio / loaned) * (loaned / borrowed)
return-rate = (reserved / borrowed) * demurrage-ratio
return-rate = reserved / borrowed
```
**The rate of return on pure bank investment is the reserve ratio.**

#### Real Banks
The independent capital ratios of all people, based on individual time preference, determine the [market](Glossary#market) rate of interest. The above substitution for the bank's own capital ratio as the interest rate implies that the bank is setting the interest rate. However this is inherent in the concept of time preference. A bank can set any level of interest it prefers. There is no assumption for real banks that the market will oblige, so market interest and therefore market returns are assumed.
```
market-return-rate = market-interest-rate * (loaned / borrowed)
market-return-rate = market-capital-ratio * (loaned / borrowed)
```
The free bank also differs from the pure bank by operational expense, which directly reduces rate of return.
```
free-bank-return-rate = market-return-rate * expense-ratio
```
The real bank only differs from the free bank by tax (inclusive of regulatory expense), which directly reduces rate of return.
```
real-return-rate = free-bank-return-rate * tax-expense-ratio
```
The central bank (state) only differs from the real bank by taxpayer subsidy (inclusive of discounted borrowing), which directly increases rate of return.
```
central-return-rate = real-bank-return-rate * subsidy-income-ratio
```
Where tax includes seigniorage of the bank money, the [Fisher Equation](https://en.wikipedia.org/wiki/Fisher_equation) must be applied above to translate the interest rate from a nominal rate to a real rate. No other change is implied other than tax, which is accounted for by the real bank above. This tax is generally the source of subsidy, which is accounted for by the central bank above.

Every [person](Glossary#person), or company of people, is a real bank, and the [state](Glossary#state) is a central bank.

A pure bank produces the service of liquid investment, an [economic good](https://en.m.wikipedia.org/wiki/Goods_and_services). The cost of production is the depreciation of its reserve. This is the pure model of all production, including labor.

A pure manufacturer has *borrowed* capital, consuming it in the manufacture of products. The consumed fraction at any time has been *loaned* to production. The unconsumed fraction at any time has been *reserved* for liquidity. The manufactured product is sold, returning *interest* ([dividend](https://en.m.wikipedia.org/wiki/Dividend)) on the consumed fraction. As manufacture requires time, and perfect efficiency is assumed, the reserve ratio declines from 100% to 0% over time. The reserve is only repopulated by more *borrowed* capital, such as by dividend reinvestment. The amount of reserve represents the same necessary productive expense as the bank’s liquidity reserve.