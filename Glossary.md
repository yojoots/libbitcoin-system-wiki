## Fundamentals
#### Person
A decision maker.
#### Machine
An instruction follower.
#### Trade
A swap of property between two [Persons](#person).

## Consensus
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
Conformance to [Consensus Rules](#consensus-rules).
#### Validation
The process of determining [Validity](#validity).
#### Enforcement
The act of discarding [Invalid](#validity) data.

## Objects
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

## Transactions
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

## Blocks
#### Timestamp
A declaration of the time of [Block](#block) production.
#### Median Time Past
An average of preceding [Block](#block) [Timestamps](#timestamp).
#### Proof
Statistical evidence of the cost of [Work](#work) performed.
#### Branch
A [Valid](#validity) sequence of [Blocks](#block).
#### Weak
A [Branch](#branch) with less cumulative [Proof](#proof) than another.
> Orphan is a misnomer for this.
#### Strong
A [Branch](#branch) with more cumulative [Proof](#proof) than another.

## Sequence
#### Confirmation
Inclusion of a [Transaction](#transaction) in a [Block](#block).
#### Unconfirmed
A [Transaction](#transaction) that does not exist in a [Block](#block).
#### Transaction Pool
The set of [Unconfirmed Transactions](#unconfirmed).
> Memory Pool is a misnomer for this.
#### Block Pool
The set of [Weak Blocks](#weak).
> Orphan Pool is a misnomer for this.
#### Genesis
The first [Block](#block) of all [Branches](#branch).
#### Depth
One more than the count of [Blocks](#block) after a [Confirmation](#confirmation).
#### Height
The count of preceding [Blocks](#block) in a [Branch](#branch).

## Money
#### Spend
The initial publication of a [Transaction](#transaction).
#### Double Spend
The [Endorsement](#endorsement) of the same [Output](#output) [Contract](#contract) by distinct [Spends](#spend).
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

## Network
#### Communication
Conveyance of data between [Machines](#machine).
#### Protocol
A set of [Communication](#communication) conventions.
#### Peer-to-Peer
A symmetrical [Protocol](#protocol).
#### Client-Server
An asymmetrical [Protocol](#protocol).
#### Latency
The delay inherent in [Communication](#communication).
#### Partition
An inability of certain [Peers](#peer-to-peer) to [Communicate](#communication).

## Components
#### Mine
A [Tool](#tool) that performs [Work](#work).
#### Drill
A [Tool](#tool) that performs [Hashing](#hash).
#### Relay
A [Tool](#tool) that disseminates new [Blocks](#block).
#### Node
A [Tool](#tool) that performs [Validation](#validation).
#### Wallet
A [Tool](#tool) that creates [Transactions](#transaction).
#### Tool
A set of [Machine](#machine) instructions.

## Actors
#### Miner
A [Person](#person) operating a [Mine](#mine).
#### Driller
A [Person](#person) operating a [Drill](#drill).
#### Relayer
A [Person](#person) operating a [Relay](#relay).
#### Merchant
A [Person](#person) accepting [Units](#unit) in [Trade](#trade).
> User is a common alias for this.
#### Owner
A [Person](#person) controlling certain [Units](#unit).
> Holder is a common alias for this.
#### Developer
A [Person](#person) implementing [Tools](#tool).

## Aggregates
#### Majority Hash Power
A subset of [Miners](#miner) with sufficient [Hash Power](#hash-power) to execute a sustained [Attack](#attack).
> 51% is a common approximation of sufficient power.
#### Economy
The set of all [Merchants](#merchant).
#### Supply
The set of all issued [Units](#unit).
#### Exchange
The [Trade](#trade) of [Units](#unit) for other property.
#### Implementation
A specific [Tool](#tool) set.

## Mining
#### Work
The process of [Block](#block) production.
#### Candidate
A potential [Block](#block) with undetermined [Proof](#proof).
#### Hash
An atomic computation to [Prove](#proof) [Candidate](#candidate) [Validity](#validity).
#### Hash Rate
The rate of [Hashing](#hash).
#### Hash Power
A fraction of the [Hash Rate](#hash-rate) of all [Mines](#mine).

## Deviations
#### Fork
A divergence in [Consensus Rules](#consensus-rules).
#### Hard Fork
A [Fork](#fork) that implies a [Split](#split).
> Expansion of the set of potentially-valid blocks.
#### Soft Fork
A [Fork](#fork) that implies a [Split](#split) unless [Enforced](#enforcement) by [Majority Hash Power](#majority-hash-power).
> Contraction of the set of potentially-valid blocks.
#### Split
A [Coin](#coin) bifurcation.
#### Reorganization
The resolution of a [Chain](#chain) bifurcation.
> Reorg is an abbreviation for this.
#### Stall
The lack of [Height](#height) increase over time.
#### Activation
Starting to [Enforce](#enforcement) a new [Rule](#rule).
#### Signal
A [Miner](#miner) indication via [Block](#block) data of intent to [Enforce](#enforcement) a new [Rule](#rule).

## Security
#### Attack
Use of [Hash Power](#hash-power) to prevent [Confirmation](#confirmation) or enable [Double Spending](#double-spend).
#### Coercion
Use of aggression to compel [Activation](#activation).
#### Distortion
Market intervention that skews the cost of [Mining](#mine).
#### Taint
Determination of [Ownership](#owner).
#### Censorship
Subjective [Confirmation](#confirmation).

## Weakness
#### Pooling
The tendency toward few [Miners](#miner) and [Relays](#relay).
> Larger mines and relays are more profitable.
#### Centralization
The tendency toward few [Merchants](#merchants).
> Merchants directly control validation.
#### Delegation
The tendency toward few [Owners](#owner).
> Owners directly control transfer.
#### Privatization
The tendency toward private [Peer](#peer-to-peer) [Communication](#communication).
> Identity implies exclusion.
#### Correlation
The ability to [Taint](#taint) by [Chain](#chain) analysis.