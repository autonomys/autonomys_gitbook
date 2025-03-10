---
description: Autonomys Network node roles and types
---

# Nodes

## Node roles

### Farmer

**Farmers** secure the [PoAS consensus](consensus/) chain by pledging disk space to the network. They are incentivized to store data through [$AI3](rewards-and-fees/) block rewards and fees. A farmer plots pieces of archival history to disk, farms the created plot for block rewards, and joins the [DSN](distributed-storage-network.md) as a data retrieval node (for syncing nodes and returning data to clients). As they do not have to store the blockchain history alongside their plot, farmers can dedicate all their available space to farming. Farmers [require](https://www.autonomys.xyz/space-acres) only an SSD drive and an off-the-shelf CPU to participate, making Autonomys one of the most accessible blockchain networks, and allowing it to become the most decentralized.

### Operator

**Operators** maintain the state of [DecEx](decoupled-execution/) chains and run computations on [domains](decoupled-execution/domains/). They are incentivized to execute transactions and manage state transitions through [$AI3](rewards-and-fees/) transaction fees.

### Timekeeper

**Timekeepers** run the [Proof-of-Time](consensus/proof-of-time.md) chain and maintain the randomness beacon for the [consensus](consensus/) chain. They are responsible for evaluating the delay function (within the target time slot duration of 1 second) and announcing the outputs to other nodes, requiring a powerful last-generation CPU. The [Subspace Foundation](https://subspace.foundation) maintains several timekeepers as a public good.

## Node types

### Full nodes

**Full nodes** process all blocks and serve peers, preserving the blockchain's state and _recent_ history for a configurable number of recent blocks until it is archived and pruned. Full nodes support newly joined nodes by providing them with the necessary block data to start their participation. Running a full node allows the participant to verify all blocks, ensuring independent auditability. All farmers, operators and timekeepers are full nodes by default.

Autonomys promotes network decentralization by keeping the hardware requirements for running full nodes low enough for an individual to set up and run one at home. The health, robustness and censorship-resistance of the Autonomys Network lies in the continuous online presence of numerous independently managed full nodes spread [across all continents of the world](https://telemetry.subspace.network).

### Archival nodes

**Archival nodes** process all blocks and serve peers, preserving the blockchain's state and _entire_ history. Archival nodes are useful for faster historical block retrieval and block explorers. All farmers, operators and timekeepers can become archival nodes. The [Subspace Foundation](https://subspace.foundation) maintains several archival nodes as a public good, but they are not necessary for the long-term functioning of the chain.

### Light nodes (clients)

**Light nodes (clients)** connect to full nodes and process block headers, but do not preserve the blockchain's state or history. Light nodes are useful for low-resource devices used by clients (users interacting with the network) and can be run in a browser with [Substrate Connect](https://github.com/paritytech/substrate-connect).
