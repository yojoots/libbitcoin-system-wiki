***
#### Person
A decision maker.
#### Machine
An instruction follower.
#### Trade
A swap of property between two [Persons](Person).
***
#### Consensus
An agreement among people.
#### Coin
A [Consensus](Consensus) regarding an acceptable medium for [Trade](Trade).
#### Consensus Rules
The set of constraints that define a [Coin](Coin).
#### Rule
A subset of [Consensus Rules](Consensus-Rules).
#### Validity
Conformance to [Consensus-Rules]().
#### Validation
The process of determining [Validity](Validity).
***
#### Unit
The atomic transferable value of a [Coin](Coin).
#### Transfer
The change of control over certain [Units](Unit).
#### Transaction
A [Valid](Validity) record of [Transfer](Transfer).
#### Block
A [Valid](Validity) set of [Transactions](Transaction) with [Timestamp](Timestamp) and [Proof](Proof).
#### Chain
The [Branch](Branch) with the most cumulative [Work](Work).
***
#### Timestamp
A declaration of the time of [Block](Block) production.
#### Median Time Past
An average of preceding [Block](Block) [Timestamps](Timestamp).
#### Proof
Statistical evidence of the cost of [Work](Work) performed.
#### Work
The process of [Block](Block) production.
#### Branch
A [Valid](Validity) sequence of [Blocks](Block).
#### Weak
A [Branch]() with less cumulative [Work](Work) than another.
#### Strong
A [Branch]() with more cumulative [Work](Work) than another.
#### Orphan
A misnomer for a [Weak Branch]().
***
#### Mine
A [Tool](Tool) that performs [Work](Work).
#### Node
A [Tool](Tool) that performs [Validation](Validation).
#### Wallet
A [Tool](Tool) that creates [Transactions](Transaction).
#### Tool
A set of [Machine](Machine) instructions.
***
#### Miner
A [Person](Person) performing [Work](Work).
#### User
A [Person](Person) accepting [Units](Unit) in [Trade](Trade).
#### Holder
A [Person](Person) controlling certain [Units]().
#### Developer
A [Person](Person) that implements [Tools](Tool).
***
#### Hash Power
The set of all [Miners](Miner).
#### Economy
The set of all [Users](User).
#### Supply
The set of all issued [Units](Unit).
#### Exchange
The [Trade](Trade) of [Units](Unit) for other property.
#### Implementation
A specific [Tool](Tool).
***
#### Subsidy
The issuance of new [Units](Unit) to a [Miner](Miner).
#### Inflation
The increase in [Supply](Supply) resulting from [Subsidy](Subsidy).
#### Fee
An implicit [Transfer](Transfer) to a [Miner](Miner).
#### Reward
The sum of [Subsidy](Subsidy) and [Fees]() for a [Block](Block).
#### Coinbase
A [Transaction](Transaction) that transfers a [Reward](Reward).
#### Halving
A reduction in the [Subsidy](Subsidy) rate (by half).
#### Difficulty
The level of [Work](Work) required for [Validity](Validity).
#### Adjustment
A change to [Difficulty](Difficulty).
#### Cap
The limit to [Supply](Supply) over all time.
#### Price
A moving average of [Exchange](Exchange) rates.
#### Capitalization
The product of [Price](Price) and [Supply](Supply).
#### Hash
[Work](Work) performed to obtain a potentially [Valid](Valid) [Block](Block).
#### Hashrate
The rate of [Hashing](Hash) by a set of [Miners](Miner).
***
#### Confirmation
Existence of a [Transaction](Transaction) in a [Block](Block).
#### Depth
One more than the count of [Blocks](Block) after a [Confirmation](Confirmation).
#### Genesis
A first [Block](Block) established by [Consensus](Consensus).
#### Height
The count of [Blocks](Block) since [Genesis](Genesis).
#### Unconfirmed
A [Transaction](Transaction) that does not exist in a [Block](Block).
#### Transaction Pool
The set of [Unconfirmed Transactions](Unconfirmed).
#### Memory Pool
A misnomer for [Transaction Pool](Transaction-Pool) subset.
#### Block Pool
The set of [Weak Blocks](Weak).
#### Orphan Pool
A misnomer for [Block Pool](Block-Pool) subset.
***
#### Script
A set of [Operations](Operation) that authorizes [Transfer](Transfer).
#### Operation
An atomic declaration of intent.
#### Contract
A [Script](Script) expressing [Transfer](Transfer) conditions.
#### Endorsement
A [Script](Script) that satisfies a [Contract](Contract).
#### Point
A reference to an [Output](Output) or [Input](Input).
#### Output
An explicit [Transfer](Transfer) and a [Contract](Contract).
#### Input
An [Output](Output) [Point](Point) and an [Endorsement](Endorsement).
#### Previous Output
The [Output](Output) to which an [Input](Input) refers.
#### Locktime
An expression of earliest [Transaction](Transaction) [Validity](Validity).