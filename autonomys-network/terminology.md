---
description: Glossary of Autonomys Network key terms
---

# Terminology

## $AI3

The [Autonomys Network](terminology.md#autonomys-network)'s native utility token needed to interact with our [AI3.0](terminology.md#ai3.0) Ecosystem. $AI3—formerly tSSC (Testnet Subspace Credits) / ATC (Auto Coin)—incentivizes the healthy operation of the network via [farmer](terminology.md#farmer) rewards and [operator](terminology.md#operator) transaction fees. $AI3 is divisible up to 18 decimal places to allow for microtransactions.

### Shannon

The smallest unit of [$AI3](terminology.md#usdai3), equal to $$10^{-18}$$$AI3 (0.000000000000000001 $AI3). Named after Claude Shannon, a mathematician, electrical engineer, and cryptographer known as the "father of information theory". Shannon's work was central to the rise of digital computing and laid the foundations for the information age.

## [AI3.0](../autonomys-vision/intro-to-ai3.md)

Decentralized, human-centric, agentic artificial intelligence.

## [Autonomys Network](architecture.md)

Hyper-scalable decentralized AI (deAI) [infrastructure stack](architecture.md) encompassing high-throughput permanent [distributed storage](terminology.md#dsn), data availability and access, and [modular execution](terminology.md#domain)—all the essential components to [build](../auto-suite/auto-sdk.md) and deploy secure super dApps (AI-powered dApps) and advanced on-chain agents.

## [Auto Suite](broken-reference)

Autonomys' product suite, including the [Auto SDK](../auto-suite/auto-sdk.md), [Auto Agents Framework](../auto-suite/auto-agents.md) and [Auto ID](../auto-suite/auto-id/) for developers, and [Space Acres](../auto-suite/spaceacres-cli/), [Astral](../auto-suite/astral/) and the [Autonomys CLI](terminology.md#autonomys-cli) for [farmers](terminology.md#farmer) and [operators](terminology.md#operator).

## Blockchain

### History

An ordered, [SCALE-encoded](https://docs.substrate.io/reference/scale-codec/) record of [Autonomys Network](terminology.md#autonomys-network) blockchain blocks.

### State

The current live status of all data stored on the [Autonomys Network](terminology.md#autonomys-network) blockchain (including wallet balances, smart contract code, etc.); the result of [operators](terminology.md#operator) executing transactions.

## Client

A user interacting with the [Autonomys Network](terminology.md#autonomys-network) through a light client such as [Substrate Connect](https://docs.substrate.io/learn/light-clients-in-substrate-connect/) or another front-end application. Clients can submit transactions and query the [state](terminology.md#state), but don't run a [node](terminology.md#node).

## [Consensus Chain](consensus/)

The [Autonomys Network](terminology.md#autonomys-network)'s [Subspace](terminology.md#subspace-protocol) ([PoAS](terminology.md#poas)) blockchain for consensus between [farmers](terminology.md#farmer). Consensus is decoupled from more computationally-intensive transaction [execution](terminology.md#decex), meaning [farming](terminology.md#farming) is lightweight and accessible, and the [consensus chain](consensus/) is quick-to-sync.

## [DecEx](decoupled-execution/)

Decoupled execution separates [consensus](consensus/) (handled by [farmers](terminology.md#farmer)) from computation (handled by [operators](terminology.md#operator))⁠, allowing for independent scaling of transaction throughput and storage. DecEx is implemented through [domains](terminology.md#domain).

## [Domains](decoupled-execution/domains/)

Modular [DecEx](terminology.md#decex) environments or [appchains](terminology.md#appchain) with shared security and data availability via [Autonomys](terminology.md#autonomys-network)' [consensus](terminology.md#consensus-chain) layer and [DSN](terminology.md#dsn). Domains support any form of computation or state transition framework, including EVM and WASM. Each domain has its own configurable runtime and gossip network (domain subnet). [Operators](terminology.md#operator) are incentivized to maintain domains with transaction/execution fees. Domains are conceptually similar to Ethereum rollups, but are integrated into the core [Autonomys Network](terminology.md#autonomys-network) protocol for horizontal scalability⁠⁠​⁠.

### Appchain

An application-specific blockchain leveraging the [Autonomys Network](terminology.md#autonomys-network) for consensus and storage. Appchains, or [domain](terminology.md#domains) chains, are customized to the needs of a specific application or use-case.

### Epoch

A block interval between each [stake](terminology.md#staking) allocation readjustment on a [domain chain](terminology.md#appchain). [Operator](terminology.md#operator) stakes are fixed for the duration of the domain epoch at its start. The stake distribution is adjusted at the end of each epoch based on new stake deposits, withdrawal requests, and slashing events.

## [DSN](distributed-storage-network.md)

Distributed storage network composed of [farmers](terminology.md#farmer) that have [plotted](terminology.md#plotting) [pieces](terminology.md#piece) of [archived history](terminology.md#archived-history) and serve them to [clients](terminology.md#client). The DSN handles data storage, retrieval and replication across the network.

## [Node](nodes.md)

A participant in [Autonomys](terminology.md#autonomys-network)' peer-to-peer (P2P) network. The main node-running roles are [farmer](terminology.md#farmer), [operator](terminology.md#operator) and [timekeeper](terminology.md#timekeeper). [Nodes](nodes.md) connects to other nodes via the P2P networking layer.

### [Farmer](../auto-suite/spaceacres-cli/farmers.md)

A [node](terminology.md#node)-running role responsible for maintaining the [history](terminology.md#history) and security of the [Autonomys Network](terminology.md#autonomys-network) [consensus chain](terminology.md#consensus-chain) and providing storage to the [DSN](terminology.md#dsn). Farmers earn [$AI3](terminology.md#usdai3) by pledging disk space to the network, [plotting](terminology.md#plotting) [pieces](terminology.md#piece) of [archived history](terminology.md#archived-history) to disk, [farming](terminology.md#farming) the created [plot](terminology.md#plot) for block and vote rewards by producing blocks for consensus, and joining the DSN as nodes for data retrieval.

#### [Autonomys CLI](https://docs.autonomys.xyz/farming/advanced-cli/install)

[Command Line Interface application](https://docs.autonomys.xyz/farming/advanced-cli/install/) for running [farmer](terminology.md#farmer) and [operator](terminology.md#operator) nodes within a terminal instance.

#### Archiving

The process of converting the [consensus blockchain](terminology.md#consensus-chain) [history](terminology.md#history) into [archived history](terminology.md#archived-history).

#### _**Raw Record**_

A fragment of [consensus blockchain](terminology.md#consensus-chain) [history](terminology.md#history)—the 'useful data' for [PoAS](terminology.md#poas) consensus—before being [archived](terminology.md#archiving).

#### _**Record**_

A [raw record](terminology.md#raw-record) that has been prepared for [archiving](terminology.md#archiving).

#### _**Archived History**_

The immutable ledger of [archived](terminology.md#archiving), ordered [consensus chain](terminology.md#consensus-chain) blocks permanently stored across the [DSN](terminology.md#dsn) in a redundant, verifiable and retrievable way.

#### _**Segment**_

A fixed-size section of (potentially partial) [consensus chain](terminology.md#consensus-chain) [history](terminology.md#history) blocks. There are two types of segment:

#### 1. _Recorded History Segment_

A [segment](terminology.md#segment) of [raw records](terminology.md#raw-record) in a buffer before [archiving](terminology.md#archiving).

#### 2. _Archived History Segment_

A [segment](terminology.md#segment) of [pieces](terminology.md#piece) of [archived history](terminology.md#archived-history) converted from a [recorded history segment](terminology.md#id-1.-recorded-history-segment) by [archiving](terminology.md#archiving).

#### _**Commitment**_

A binding, cryptographic commitment to the value and integrity of a specific piece of data that allows the committer ([nodes](terminology.md#node)) to conceal the committed value and reveal it later. Others can then verify that the committed value matches the original commitment.

The [Autonomys Network](terminology.md#autonomys-network) uses two types of commitment:

* **Record Commitment:** a KZG polynomial commitment to the blockchain data in a [raw record](terminology.md#raw-record).
* **Segment Commitment:** a KZG polynomial commitment to hashes of all record commitments in an [archived history segment](terminology.md#id-2.-archived-history-segment).

#### _**Segment Header**_

A compact header in an [archived history segment](terminology.md#id-2.-archived-history-segment) containing the [segment](terminology.md#segment) index, segment [commitment](terminology.md#commitment), a pointer to the previous segment header, and information about the progress of block [archiving](terminology.md#archiving).

#### _Witness_

A cryptographic proof of the existence of a specific piece of data within a larger dataset, such as a Merkle tree or polynomial [commitment](terminology.md#commitment). Witnesses are used in the [Subspace Protocol](terminology.md#subspace-protocol) to efficiently verify the inclusion of data in a [plot](terminology.md#plot) or blockchain [history](terminology.md#history) without requiring access to the entire dataset, enabling [farmers](terminology.md#farmer) and [operators](terminology.md#operator) to validate data integrity while minimizing bandwidth and computational overhead.

#### (Re)Plotting

The process of [farmers](terminology.md#farmer) creating (and maintaining) [plots](terminology.md#plot) of [archived history](terminology.md#archived-history) on their disk, allowing for efficient [PoAS](terminology.md#poas) consensus and retrievability of archived history.

#### _**Piece**_

A unit of [archived history](terminology.md#archived-history) from which [archived history segments](terminology.md#id-2.-archived-history-segment) are composed. Each piece is composed of a [record](terminology.md#record), a [commitment](terminology.md#commitment), and a [witness](terminology.md#witness).

#### _**Sector**_

A set of encoded [pieces](terminology.md#piece) written to disk during [plotting](terminology.md#re-plotting). A sector contains encoded the [record](terminology.md#record) data from the pieces, the original piece [commitments](terminology.md#commitment), [witnesses](terminology.md#witness), and other metadata about stored pieces.

#### _**Plot**_

A collection of [sectors](terminology.md#sector) that can be used for [farming](terminology.md#farming).

#### Farming

The process of [farmers](terminology.md#farmer) participating in [Subspace](terminology.md#subspace-protocol) consensus by competing to solve a puzzle using their [plots](terminology.md#plot). Farmers farm a block and earn [$AI3](terminology.md#usdai3) rewards when they are the first to solve the puzzle and submit a valid proof.

#### Reconstruction

The process of reconverting [archived history segments](terminology.md#id-2.-archived-history-segment) to [recorded history segments](terminology.md#id-1.-recorded-history-segment) for seeding new [nodes](terminology.md#node).

### [Operator](../auto-suite/spaceacres-cli/operators.md)

A [node](terminology.md#node)-running role responsible for running computation on [domains](terminology.md#domains) on the [Autonomys Network](terminology.md#autonomys-network). [Staked](terminology.md#staking) operators earn [$AI3](terminology.md#usdai3) by providing compute to the network, running [state](terminology.md#state) transitions, maintaining state by bundling transactions, validating state [commitments](terminology.md#commitment), and deterministically executing transaction bundles on [domain chains](terminology.md#appchain) in the order defined by the [farmers](terminology.md#farmer)' [consensus chain](terminology.md#consensus-chain) in exchange for transaction/compute fees from [clients](terminology.md#client).

#### Leader Operator

Selected through an [$AI3](terminology.md#usdai3) [stake](terminology.md#staking)-weighted VRF (Verifiable Random Function) election process to produce bundles for a [domain](terminology.md#domains) in a specific time slot⁠.⁠

#### [Staking](decoupled-execution/staking.md)

The process of [nominators](terminology.md#nominator) pledging [$AI3](terminology.md#usdai3) towards [operators](terminology.md#operator) on [domains](terminology.md#domains) in exchange for rewards, locking it up as collateral to support the operation and security of the [Autonomys Network](terminology.md#autonomys-network).

### [Timekeeper](consensus/proof-of-time.md)

A [node](terminology.md#node)-running role responsible for running the [Proof-of-Time](consensus/proof-of-time.md) chain and maintaining the randomness beacon for the [Autonomys Network](terminology.md#autonomys-network) [consensus chain](terminology.md#consensus-chain).

## [Nominator](../auto-suite/spaceacres-cli/operators.md)

[$AI3](terminology.md#usdai3) holders that [nominate](../auto-suite/spaceacres-cli/operators.md) tokens towards [operators](terminology.md#operator) and earn a share of the fees as [staking](terminology.md#staking) rewards.

## [PoAS](consensus/)

[Proof-of-Archival-Storage](consensus/), the [Autonomys Network](terminology.md#autonomys-network)'s custom proof-of-capacity [consensus](terminology.md#consensus-chain) mechanism.

## [Subspace (Protocol)](https://autonomys.xyz/solution)

The [Autonomys Network](terminology.md#autonomys-network)'s unique [Proof-of-Archival-Storage (PoAS)](terminology.md#poas) consensus mechanism.
