***
#### Person
A decision maker.
#### Machine
An instruction follower.
#### Trade
A swap of property between two [Persons](#person).
***
#### Consensus
An agreement among [People](#person).
#### Coin
A [Consensus](#consensus) regarding a mutually-acceptable medium for [Trade](#trade).
> Bitcoin is a Coin
#### Consensus Rules
The set of constraints that define a [Coin](#coin).
#### Rule
A subset of [Consensus Rules](#consensus-rules).
#### Validity
Conformance to [Consensus-Rules](#consensus-rules).
#### Validation
The process of determining [Validity](#validity).
***
#### Unit
The atomic transferable value of a [Coin](#coin).
> The Satoshi is the Bitcoin Unit
#### Transfer
The change of control over certain [Units](#unit).
#### Transaction
A [Valid](#validity) record of [Transfer](#transfer).
#### Block
A [Valid](#validity) set of [Transactions](#transaction) with [Timestamp](#timestamp) and [Proof](#proof).
#### Chain
The [Branch](#branch) with the most cumulative [Proof](#proof).
***
#### Timestamp
A declaration of the time of [Block](#block) production.
#### Median Time Past
An average of preceding [Block](#block) [Timestamps](#timestamp).
#### Proof
Statistical evidence of the cost of [Work](#work) performed.
#### Work
The process of [Block](#block) production.
#### Branch
A [Valid](#validity) sequence of [Blocks](#block).
#### Weak
A [Branch](#branch) with less cumulative [Proof](#proof) than another.
#### Strong
A [Branch](#branch) with more cumulative [Proof](#proof) than another.
#### Orphan
A misnomer for a [Weak Branch](#weak).
***
#### Mine
A [Tool](#tool) that performs [Work](#work).
#### Node
A [Tool](#tool) that performs [Validation](#validation).
#### Wallet
A [Tool](#tool) that creates [Transactions](#transaction).
#### Tool
A set of [Machine](#machine) instructions.
***
#### Miner
A [Person](#person) performing [Work](#work).
#### User
A [Person](#person) accepting [Units](#unit) in [Trade](#trade).
#### Holder
A [Person](#person) controlling certain [Units](#unit).
#### Developer
A [Person](#person) that implements [Tools](#tool).
***
#### Hash Power
The set of all [Miners](#miner).
#### Economy
The set of all [Users](#user).
#### Supply
The set of all issued [Units](#unit).
#### Exchange
The [Trade](#trade) of [Units](#unit) for other property.
#### Implementation
A specific [Tool](#tool).
***
#### Subsidy
The issuance of new [Units](#unit) to a [Miner](#miner).
#### Inflation
The increase in [Supply](#supply) resulting from [Subsidy](#subsidy).
#### Fee
An implicit [Transfer](#transfer) to a [Miner](#miner).
#### Reward
The sum of [Subsidy](#subsidy) and [Fees](#fees) for a [Block](#block).
#### Coinbase
A [Transaction](#transaction) that [Transfers](#transfer) a [Reward](#reward).
#### Maturity
The [Depth](#depth) at which a [Coinbase](#coinbase) [Output](#output) becomes [Transferable](#transfer).
#### Halving
A reduction in the [Subsidy](#subsidy) rate (by half).
#### Difficulty
The level of [Proof](#proof) required for [Validity](#validity).
#### Adjustment
A change to [Difficulty](#difficulty).
#### Cap
The limit to [Supply](#supply) over all time.
#### Price
A moving average of [Exchange](#exchange) rates.
#### Capitalization
The product of [Price](#price) and [Supply](#supply).
#### Hash
[Work](#work) performed to obtain a potentially [Valid](#validity) [Block](#block).
#### Hashrate
The rate of [Hashing](#hash) by a set of [Miners](#miner).
***
#### Confirmation
Existence of a [Transaction](#transaction) in a [Block](#block).
#### Depth
One more than the count of [Blocks](#block) after a [Confirmation](#confirmation).
#### Genesis
The first [Block](#block) of all [Branches](#branch).
#### Height
The count of preceding [Blocks](#block) in a [Branch](#branch).
#### Unconfirmed
A [Transaction](#transaction) that does not exist in a [Block](#block).
#### Transaction Pool
The set of [Unconfirmed Transactions](#unconfirmed).
#### Memory Pool
A misnomer for [Transaction Pool](#transaction-pool) subset.
#### Block Pool
The set of [Weak Blocks](#weak).
#### Orphan Pool
A misnomer for [Block Pool](#block-pool) subset.
***
#### Script
A set of [Operations](#operation) that authorizes [Transfer](#transfer).
#### Operation
An atomic declaration of intent.
#### Contract
A [Script](#script) that expresses [Transfer](#transfer) conditions.
#### Endorsement
A [Script](#script) that satisfies a [Contract](#contract).
#### Point
A reference to an [Output](#output) or [Input](#input).
#### Output
An explicit [Transfer](#transfer) and a [Contract](#contract).
#### Input
An [Output](#output) [Point](#point) and an [Endorsement](#endorsement).
#### Previous Output
The [Output](#output) to which an [Input](#input) refers.
#### Locktime
An expression of earliest [Transaction](#transaction) [Validity](#validity).
***
#### Fork
A divergence in [Consensus Rules](#consensus-rules).
#### Split
The [Chain](#chain) bifurcation resulting from a [Fork](#fork).
#### Stall
The lack of [Height](#height) increase over time.
#### Signal
A [Miner](#miner) indication of [Fork](#fork) preference.
#### Activation
The act of adding a [Rule](#rule).