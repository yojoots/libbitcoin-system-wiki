Blockstream has announced a network that, "[broadcasts the Bitcoin blockchain from space](https://blockstream.com/satellite)." There are several use cases outlined in a [FAQ](https://blockstream.com/satellite/faq):

## Free Services
The company provides the equivalent of a single [node](Glossary#node) on the [peer-to-peer](Glossary#peer-to-peer)  network. Nearly any [person](Glossary#person) on Earth can connect to this node using an inexpensive receiver. In the initial deployment the node broadcasts but does not receive.

#### New Bitcoin Users
> More people participating in bitcoin means a more decentralized network... [M]akes bitcoin more robust and bullet-proof...

To the extent that this enables new users it implies those users are entirely dependent on this one node. If the user already has access through the Internet (for example) it is not new participation.

#### Covert Bitcoin Usage
> [I]nternet traffic patterns from running a node can identify you as a bitcoin user. [T]here’s no internet involved to receive the blockchain data, so your patterns are private to you.

To the extent that this enables covert use it implies such users are entirely dependent on this one node. The scenario precludes redundant access through the Internet (for example) unless it is also private, but presumes that not to be the case.

#### Partition Resistance
> Without [redundancy] your ability to use the bitcoin network is limited, including your security against sybils... [P]rovides a redundant connection to the blockchain that doesn’t require internet. 

To the extent that this is necessary it implies that users are almost entirely dependent on this one node. Otherwise access through the Internet (for example) does not suffer from persistent "limiting" of usability.

## Paid Services
The company plans to charge for the following services. It is not reasonable to expect *any* services be offered for free, however it is important to the strength of [consensus](Glossary#consensus) for people to understand [centralization](Centralization-Risk) and [pooling pressure](Pooling-Pressure-Risk) risks.

#### Web (sky) API
> We have plans to extend the network over time to be an open platform for application developers to build on.

There are no details presently. However, in the case where each person [validates](Glossary#validation), a *Bitcoin* API must exist over that person's node, not over a third party service. Otherwise the service is a manifestation of [centralization](Glossary#centralization). Exceptions would be acceptance of [transactions](Glossary#transaction) and publication of [exchange](Glossary#exchange) rates.

#### Payment Processor
> When we make available advanced features, capabilities, and services intended for business use, we plan on monetizing those.

There are no details presently. It is possible that these services do not fall into the category of payment processor, but this is the common model of Bitcoin business services. Payment processors take over validation and potentially wallet services for the business, a manifestation of centralization.

#### Mining Relay
> Bitcoin mining is more delay sensitive and access to lower delay signals optimized for mining is one of the future services we plan to charge for.

The intent of this service is [clear](https://github.com/libbitcoin/libbitcoin/wiki/translation-of-bitcoin-satellite-mining-decentralization). It is proposed that a [relay](Glossary#relay) service will provide sufficiently low latency for competitive [mining](Glossary#mine). As detailed in [Relay Fallacy](Relay-Fallacy), a relay service is a [pooling](Glossary#pooling) manifestation.

## Summary

It is possible that other similar networks may be deployed by independent operators. This would resolve the dependency on the single node. Nevertheless, success implies that a substantial number of people will become entirely dependent upon just a few nodes, all operating with [state](Glossary#state) licenses. Ironically, people without useful Internet service would be accepting a persistent [Sybil attack](https://en.wikipedia.org/wiki/Sybil_attack) and [partitioning](Glossary#partitioning) themselves from all but these few nodes.

This is not comparable to having a similarly small number of Internet providers, since in that case thousands of independently operated nodes are potentially reachable through any number of protocols. As such the most compelling *free services* scenario may be North Korea, where Internet is [generally unavailable](http://www.bbc.com/news/world-asia-37426725) and the risk of a dependency on a few licensed satellite providers may be a reasonable trade-off against oppressive [currency controls](https://en.wikipedia.org/wiki/Foreign_exchange_controls).

It is suggested that public monitoring mitigates the potential for foul play:

> Anyone is free to compare the blockchain... from any other source to verify that the broadcast is accurate and has not been tampered with.

However the only way for this monitor to provide verifiable information is for it to effectively be an independent node, which requires the satellite service user to have a redundant connection.

It is certain that one of the three *paid services* is pooled, and likely that the other two are centralized. This is not surprising, as typically where there is a service fee for Bitcoin participation there is a point of [aggregation](Glossary#aggregation), which works against Bitcoin security by limiting [risk sharing](Risk-Sharing-Principle).