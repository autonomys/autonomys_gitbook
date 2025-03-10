---
description: An overview of how the Autonomys Network advances blockchain technology
---

# Advancing Blockchain

Autonomys' Subspace Protocol is designed from first principles to resolve several critical challenges associated with blockchain technology.

## Resolving the blockchain trilemma

The Autonomys Network resolves the blockchain trilemma—simultaneously achieving [scalability](scalability.md), [security](consensus/security.md) and decentralization—by utilizing accessible SSD-based [PoAS consensus](consensus/), and independently scaling storage, transaction throughput, and bandwidth. This balanced approach means none of the key properties of a healthy blockchain network are sacrificed.

<figure><img src="../.gitbook/assets/Trilemma_Isolated_1 (1) (1).png" alt=""><figcaption><p>The blockchain trilemma</p></figcaption></figure>

## Resolving the farmer's dilemma & increasing accessibility

In an effort to make blockchains more energy-efficient, egalitarian and decentralized, several protocols employ [proof-of-capacity (PoC)](introduction.md)-based consensus that replaces compute-intensive mining with storage-intensive farming. PoC consensus introduces a unique mechanism design challenge known as the 'farmer's dilemma', which suggests that existing constructions are not in fact incentive-compatible. In short, farmers must decide whether to allocate scarce storage resources to maintain the chain state and history, or maximize the amount of space they pledge towards consensus. Rational farmers (seeking maximum rewards) will always choose the latter, at best becoming light nodes, while at worst encouraging pooled farming under a few trusted operators.

<figure><picture><source srcset="../.gitbook/assets/Farmers_Dilemma-dark (1).svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/image (9).png" alt=""></picture><figcaption><p>The farmer's dilemma</p></figcaption></figure>

To resolve this dilemma, Autonomys farmers maintain only minimal state and history, while retaining the security properties and decentralization benefits of being a full node. Farmers store the blockchain history collectively, many times over, with each farmer storing as many replicas as their disk space allows. Autonomys Network consensus is based on [Proof-of-Archival-Storage (PoAS)](consensus/)—farmers' proofs of their replicated storage of the blockchain history.&#x20;

The [Subspace Protocol](consensus/) decouples consensus and execution/computation, meaning farmers only propose the ordering of transactions, while staked operators maintain the state and compute transitions. This node role separation significantly reduces the storage and compute requirements for running a farmer node—even in an Ethereum-style execution model—allowing for higher levels of participation.

<figure><picture><source srcset="../.gitbook/assets/Farmers_Dilemma_Solution-dark (1).svg" media="(prefers-color-scheme: dark)"><img src="../.gitbook/assets/image (10).png" alt=""></picture><figcaption><p>How Autonomys resolves the farmer's dilemma</p></figcaption></figure>

## Eliminating blockchain bloat

The [Subspace Protocol](consensus/) is designed to overcome the critical issue of blockchain bloat—the tendency of blockchains to become more centralized over time, especially as they scale. Bloat is the result of every full node storing the chain's entire transaction history and resulting execution state.

Autonomys eliminates bloat by uniquely combining the best parts of Layer-1 blockchains including Ethereum, Filecoin and Chia into a new network with a novel storage-based PoAS consensus protocol, permanent distributed storage infrastructure, and scalable decoupled execution framework.

## Addressing state bloat

To resolve the problem of state bloat, Autonomys introduces a [decoupled execution (DecEx) framework](decoupled-execution/). DecEx separates the probabilistic process of coming to consensus over ordering transactions from the deterministic process of executing them. Farmer nodes confirm the availability of transactions and provide an ordering, while a secondary network of staked operator nodes executes the transactions and maintains the resulting chain state.

Decoupling these roles permits different hardware requirements for each node type, allowing farming to remain lightweight and open to anyone, while also providing a foundation for scaling execution both vertically—based on the hardware capabilities of operators—and horizontally—by later partitioning operators into different namespaced execution domains.

## Scaling blockspace

Blockspace is space on a blockchain that can run code or store data. The overall execution throughput of a blockchain is ultimately constrained by the blockspace bandwidth.  To achieve optimal throughput, our [scalability](scalability.md) framework seeks to increase the blockspace linearly as more nodes contribute resources to the network—without reducing security or decentralization.

The Autonomys Network achieves optimal scalability through Orthogonal Execution (OE) by first horizontally scaling the blockspace of the base data availability layer and then vertically scaling the transaction throughput for each domain. OE starts with the unique properties of the Subspace Protocol and extends them with several ideas originating within the Tse Lab at Stanford University. These include the Prism protocol for vertical scaling and the Semi-AVID-PR scheme for distributed data availability.

## Aligning incentives for optimal scalability

In order to economically secure the network in an open environment, Autonomys uses a novel algorithm that dynamically adjusts the cost of blockspace in response to changes in supply and demand, naturally keeping the network [incentive-compatible](rewards-and-fees/) for both farmers (providing storage and data availability bandwidth) and operators (providing raw compute power).

The Autonomys Network represents the world's first two-sided marketplace for blockspace, enabling a dynamic on-chain cost-of-blockspace and a stable off-chain price-of-blockspace without relying on centralized control or coordination. On one side are farmers, who collectively supply blockspace bandwidth through their storage of the blockchain history, and on the other side are dApp developers and users, who demand blockspace to deploy, run and use applications.

Autonomys' marketplace algorithm automatically adjusts the on-chain cost-of-blockspace paid out to farmers based on real-time supply and demand. When demand is high, the cost rises to incentivize more farmers to join. When demand is low, the cost falls to disincentivize over-investment in storage. This dynamic adjustment process occurs transparently on-chain through the protocol rules. By combining this approach with existing scalability frameworks, Autonomys can achieve linear scaling of the blockspace as more nodes join the network, without sacrificing security or decentralization.

## Conclusion: From Web3 to AI3.0

The Autonomys Network represents a dual solution to both the:

• challenges of security, decentralization, verifiability and scalability facing web3 infrastructure—embodied in the farmer’s and verifier’s dilemmas, and the blockchain trilemma.

• risks and opportunities posed by the emerging AI-augmented world.

In implementing our cutting-edge blockchain technologies, we have not only built a robust, decentralized system that addresses the immediate challenges of permanent storage, provenance and compensation for AI training data, but through our verifiable AI3.0 infrastructure and Auto ID, also laid the groundwork for a future where humans and Autonomys Agents can interact in a transparent, secure, and trustworthy manner.
