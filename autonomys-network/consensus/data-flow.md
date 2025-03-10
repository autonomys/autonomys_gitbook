---
description: The flow of data through the Autonomys Network
---

# Data Flow

From the moment a transaction is submitted to the Autonomys Network to the point it is permanently archived, data goes through several stages:

1. A transaction is validated and included in a consensus chain block directly or through the inclusion of [domain](../decoupled-execution/domains/) bundles.
2. The transactions and bundles in the block are executed, activating a global domain state change.
3. Once the block reaches a certain depth (currently 100 blocks), it is [archived](proof-of-archival-storage/archiving.md) alongside other blocks, becoming part of the chain's archival history.
4. Newly archived pieces are added to [farmers](../network-architecture.md)' caches through the [distributed storage network (DSN)](../distributed-storage-network.md) and replicated multiple times throughout the network.
5. Pieces are encoded into farmer [plots](proof-of-archival-storage/plotting.md) on disk for permanent storage.
6. When a client requests the archived transaction data, the original data is reconstructed from archived pieces on the fly.

<figure><img src="../../.gitbook/assets/infographic-blockchain-data-flow (1).png" alt=""><figcaption><p>Blockchain Data Flow</p></figcaption></figure>

## Blocks

### Block structure and limits

A PoAS consensus chain block follows the general structure of a standard blockchain block—it consists of a body and a header, and points to a parent block. Consensus chain block headers contain metadata about the block that allows for the verification of the chain's [security](security.md), while the body contains transactions and domain bundles. Transactions include transfers, votes and fraud proofs. Domain bundles are sets of transactions from a particular domain (e.g., [Auto EVM](../decoupled-execution/domains/auto-evm.md) contract calls).

Each block has a certain length and weight. Length is the amount of storage a block consumes on the network—equal to the size of the encoded transactions and bundles in the block body in bytes. Weight is the estimated time it would take to execute a block—equal to the sum of the compute weights of all the transactions in the body. Currently, consensus chain blocks are limited to 3.75 MiB of length and 1.5 seconds of compute weight for normal user transactions (with up to 1.25 MiB and 0.5 seconds extra for system extrinsics like votes or chain updates).

### Consensus chain block headers

Consensus chain block headers contain the:

* Block number in the chain of blocks
* Hash of the parent block
* Merkle root of the trie of extrinsics included in this block
* Merkle root of the state trie after processing this block
* Time slot number claimed by the block producer
* Global randomness at the claimed time slot (derived from the [proof-of-time (PoT)](proof-of-time.md) chain)
* Solution to the slot challenge for the claimed time slot (includes a winning chunk of history, a proof-of-space for the farmer's plot, and a KZG witness that the winning chunk is part of the archival history at the claimed height)
* Solution range used to find the winning chunk of history
* Signature of the farmer over the header

### Domain bundles

A bundle contains multiple transactions from a particular domain (e.g., Auto EVM contract calls) deterministically ordered for efficient execution, propagation and inclusion in blocks. Bundles contain a signed header and a list of transactions. A bundle header contains the:

* Domain ID (e.g., Auto EVM)
* Operator ID of the bundle producer
* Merkle root of the trie of transactions included in this bundle
* Execution receipt that should extend the domain receipt chain
* Size of the bundle body in bytes (to calculate the storage cost)
* Total estimated weight of all extrinsics in the bundle (to prevent overloading the bundle with compute)
* Time slot claimed by the bundle
* Global randomness at the claimed time slot (derived from the PoT chain)
* Proof-of-election of the operator as bundle producer for the claimed time slot (based on the slot challenge and the operator's stake in the current epoch)

Each domain bundle can be visualized as 'a block inside a block', with its bundle header containing information about the domain and the bundle producer. Any consensus chain block may contain many bundles from different domains without burdening the consensus layer, as farmers check if bundles are well-formed and package them within a block, but do not execute any of the computations inside them.

### Domain blocks

Domains are application-specific blockchains (app-chains) with separate namespaced execution environments that rely on the consensus chain for shared security, data availability, settlement, and interoperability. Domain chains consist of domain blocks that only contain bundles relevant to their domain.&#x20;

<figure><picture><source srcset="../../.gitbook/assets/Slot_To_Execution-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/image (12).png" alt=""></picture><figcaption></figcaption></figure>
