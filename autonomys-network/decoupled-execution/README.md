---
description: An overview of Autonomys' decoupled execution framework and domains
---

# Decoupled Execution (DecEx)

## Overview

The Autonomys Network decouples consensus from computation by separating transaction execution into independent environments (_domains_) run by [operator nodes](./#operator) pledging sufficiently powerful hardware and staking $AI3. Transactions and smart contract calls from Autonomys dApps and Auto Agents are executed on these domains. Operators are incentivized through [execution fees](../rewards-and-fees/) (similar to Ethereum gas fees).

[Domains](domains/) are essentially built-in rollups that support any conceivable state transition framework and smart contract execution environment, making deploying a domain as easy as deploying a smart contract. They allow builders to easily launch their own network without bootstrapping a new validator set, while still benefiting from the shared security and interoperability provided by the Autonomys Network consensus chain.

Our decoupled execution system allows for significant scalability improvements over monolithic execution environments (like Ethereum) by independently scaling transaction throughput and storage capacity. It preserves the security properties of the Nakamoto consensus, even in the presence of a dishonest majority of operators, given an honest majority of farmers on the [consensus layer](../consensus/). Our approach provides a unique solution to the challenges faced by storage-based blockchains, offering a balance between permissionless farming and permissioned staking. Unlike hybrid PoC/PoS consensus mechanisms employed by other storage-based blockchains, Autonomys’ system clearly distinguishes between a permissionless [farming](../consensus/proof-of-archival-storage/farming.md) mechanism for block production and a permissioned [staking](staking.md) mechanism for block finalization.

By simultaneously addressing the farmer’s dilemma, verifier’s dilemma, and blockchain bloat issues, the Autonomys Network presents a comprehensive solution to several critical challenges in the web3 industry, at the same time as making blockchains more energy-efficient, egalitarian and decentralized, and maintaining the security and functionality necessary for complex [smart contract](domains/auto-evm.md) and [application development](../../auto-suite/auto-sdk.md).

## Design challenges

It is safe to assume that rational farmers will seek to dedicate all their available disk space to consensus and expend as little computation as possible, while remaining on the longest valid chain, meaning they must compute all intermediate state transitions and maintain the state. As the burden of maintaining the state and computing transitions grows larger, both the farmer’s and verifier’s dilemmas present themselves, leading economically rational farmers to sacrifice security for higher rewards at a lower cost, by either becoming light clients or joining a trusted farming pool.

## Autonomys' solution

To resolve these dilemmas, we implement a method that relieves farmers of this burden, while still allowing them to be certain they are extending the longest valid chain. Critically, this method does not degrade the liveness, fairness, or safety of block production. Our solution follows the classic technique in distributed systems of decoupling consensus and computation.

In this system, farmers are solely responsible for providing subjective and probabilistic consensus over the ordering of transactions. A separate class of executor nodes—operators—computes the objective and deterministic result of that ordering. Operators are selected through a stake-based election, separate from block production, analogous to the block finalization technique proposed by [Casper FFG](https://doi.org/10.48550/arXiv.1710.09437). They are incentivized by transaction fees shared with farmers, and held accountable through a system of non-interactive [fraud proofs](https://doi.org/10.48550/arXiv.1809.09044) and [slashing](https://blog.ethereum.org/2014/01/15/slasher-a-punitive-proof-of-stake-algorithm).

This approach, while influenced by [Flow](https://doi.org/10.48550/arXiv.1909.05821) ([see](https://doi.org/10.48550/arXiv.2002.07403) [also](https://doi.org/10.48550/arXiv.1909.05832)), is simpler (using two, not four, classes of nodes), retains compatibility with Nakamoto consensus, and maintains the ‘honest _majority_ of farmers’ and ‘honest _minority_ of operators’ security assumptions. It also draws inspiration from [Truebit](https://doi.org/10.48550/arXiv.1908.04756), recognizing that optimistic off-chain computation with fallbacks to on-chain verification could realize a trustless decentralized mining pool. Unlike protocols such as [ChainSpace](https://doi.org/10.48550/arXiv.1708.03778) and [LazyLedger](https://doi.org/10.48550/arXiv.1905.09274), which achieve decoupling by delegating computation to clients, our system retains global state, allowing for cross-contract calls and composability of applications.

Under the decoupled execution (DecEx) framework, farmers only confirm the availability of transactions and provide an ordering, while secondary networks of staked operator nodes execute the transactions and maintain the resulting chain states. DecEx separates the probabilistic process of coming to a consensus over the ordering of transactions from the deterministic process of executing these ordered transactions. The decoupling of these roles permits alternative hardware requirements for different node types, allowing us to keep farming lightweight and open to anyone, while also providing a foundation for scaling execution both vertically—based on the hardware capabilities of operators—and horizontally—by partitioning operators into different namespaced execution domains.

<figure><img src="../../.gitbook/assets/infographic-domain-transaction-flow (1).png" alt=""><figcaption><p>Domain transaction flow from submission to fee distribution</p></figcaption></figure>

## Contents

Read the following subsections for technical details of decoupled execution, domains, staking and the Auto EVM:

1. [Domains](domains/)
   1. [Taxonomy](domains/taxonomy.md)
   2. [Auto EVM](domains/auto-evm.md)
2. [Staking](staking.md)

## [Domains](domains/)

While conceptually similar to rollups on Ethereum, such as Optimism, DecEx domains differ heavily in their protocol implementation. Unlike Ethereum, the Autonomys Network does not have a global smart contract execution environment within the core protocol. Instead, DecEx is enshrined within the semantics of the core protocol itself. Despite being implemented at the protocol level, DecEx domains are still able to provide rollup protocol designers with a flexible system capable of supporting any state transition integrity framework for verifying the receipt chain, including optimistic fraud proofs and zero-knowledge proofs. Domains support any smart contract execution environment that can be implemented within the Substrate framework, including the Ethereum Virtual Machine (EVM) and Web-Assembly (WASM).

Domains are the logical extension of the basic DecEx framework, taking it from a single, monolithic execution environment to a modular, interoperable network of namespaced execution environments. Each domain is its own programmable layer-2 rollup, or configurable application-specific blockchain (app-chain), that relies on the consensus chain for consensus, decentralized sequencing, data availability, and settlement. However, a smart contract, (super) dApp, or agent can use multiple domains to achieve a complex task, enabled by our unique cross-domain communication.

## [Roles](../nodes.md)

### Farmer

In our DecEx model, users submit execution transactions directly to operators, who pre-validate and batch these transactions into bundles through a (probabilistic) stake-weighted election process. These bundles are then submitted to farmers, who treat them as base-layer transactions. Farmers only verify the proof-of-election and ensure the data is available, before batching bundles into blocks in the usual manner. When a farmer finds a PoAS solution that satisfies the storage audit, they order valid transactions into a new block, committing to the last valid state root proposal they observe. Unlike on Ethereum and most other L1s, farmers do not need to maintain the code, state or account balances for contracts, only the smaller set of balances and nonces for externally owned accounts (EOAs), and minimal information about each domain runtime, staked operators, and execution receipt (ER) chains. The farmer network effectively provides decentralization-as-a-service to the domains.

### Operator

Operator nodes maintain the full state of their respective domain and execute transactions, returning new proposed state roots. For each new block, a small constant number of operators are chosen through a stake-weighted election. Execution transactions from the block are then ordered deterministically, using a secure cryptographic shuffle based on the unique PoAS produced by the farmer. Operators execute the transactions according to this ordering, and produce a deterministic state commitment in the form of an execution receipt, incrementally committing to intermediate state roots. These state commitments are then included in the next bundle, forming a deterministic receipt chain tracked by all farmers within the consensus chain protocol. The initial, default implementation of DecEx employs an optimistic fraud-proof validation scheme.

## Decentralized sequencing

Once the bundled transactions are included in the consensus block by farmers, domain operators must execute them in a deterministic order based on a verifiably random seed from the consensus chain. This absolves the operators of the responsibility of sequencing user transactions, while also preventing them from harvesting the maximal extractable value (MEV) and causing economic harm to users. Bundled transactions from a domain are opaque to the farmer block proposer as the latter does not have the domain state. Thus, the farmer cannot participate in MEV extraction either. Neither the order in which the operator batches the transactions in the bundle nor the order of bundles in the consensus block influences the final sequencing for execution.

## Liveness

To retain liveness in case of network asynchrony or byzantine actors, operator elections are re-run for each new time slot. This allows newly elected operators to include past ERs to catch up. The election threshold dynamically adjusts based on observed operator availability. Each domain may specify the frequency of re-election based on its own needs and demand, without interfering with the liveness of other domains or the consensus chain.

## Fairness

Fairness is preserved through a fair compensation mechanism between farmers and operators. Farmers are compensated for their blockspace at the current price of storage, by rewards, and for their work of including the domain bundles, by the operators. Operators are compensated for the blockspace costs incurred if their ERs are valid, and for their work of bundling and executing user transactions, via transaction fees.

## Validity

Validity is ensured through a system of fraud proofs. Within the challenge period, any honest node which operates on a domain can compile a fraud proof for an invalid state transition performed by another operator on that domain. The fraud proof can be verified by any consensus node without having the whole domain state. If it is valid, the operator who proposed the invalid ER will have their entire deposit confiscated. Any operator who has extended the invalid ER is also slashed as punishment for dishonest or lazy behavior.

## Finality

Transactions on optimistic domains are subject to a challenge period until they are settled on the consensus chain. During the challenge period, nodes can dispute the correctness of state transitions presented by operators. Any node that has an up-to-date state of the domain can submit fraud proofs for this domain and does not need to be a staked operator to do so. Whether the node is acting honestly or not in this particular instance is determined by the validity of the fraud proof. Currently, the challenge period on domains is 14400 blocks, or approximately 1 day. Fast finality is possible for services that run their own honest operator nodes. Since the operator nodes execute all the state transitions, they can be certain about the correctness of the domain state at any given time.

## Safety

Safety is maintained by distinguishing between illegal and invalid transactions. Farmers enforce legality by ensuring transactions have valid signatures and can cover the specified fees. Operators enforce validity by executing transactions deterministically in the order specified by farmers.

## Network dynamics

Our system is able to account for network delays and stochastic block production. Operators are incentivized to generate fraud proofs locally to release their own ERs as soon as possible, speeding up fraud-proof propagation and strengthening security guarantees. Farmers order by urgency and deduplicate fraud proofs in their mempool to ensure timely inclusion.

## Adversarial scenarios

The system is designed to handle various adversarial scenarios, including attempts to attack the liveness of execution or confuse farmers about transaction legality. Even in the presence of a dishonest majority of operators, the system remains secure as long as a single honest operator remains connected to an honest farmer within their peer set. Operators are incentivized to reveal fraud to protect their own stake and claim their share of the rewards, while they are punished for extending an invalid ER without first demonstrating fraud.

<figure><picture><source srcset="../../.gitbook/assets/Domain_Chains-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/image (24).png" alt="" width="509"></picture><figcaption><p>Domains</p></figcaption></figure>
