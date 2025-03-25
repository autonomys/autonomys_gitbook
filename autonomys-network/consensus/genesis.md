---
description: The creation of the Autonomys Network consensus chain
---

# Genesis

The genesis process of Autonomys' consensus chain (launched on mainnet in November 2024) involved initializing and configuring the blockchain's starting state to ensure its functionality, following these steps:

1. **Genesis Configuration**: Creating a genesis configuration defines the blockchain's initial parameters, including the consensus parameters, initial balances, boot nodes, and network protocol settings.
2. **Genesis Block Creation**: After the configuration is complete and the initial state is defined, the genesis block is created. Randomly generated data the size of one segment (128MiB) is attached to the serialized encoding of the genesis block to bootstrap step 4.
3. **Proof-of-Time Initialization**: [Timekeepers](../nodes.md) initialize the randomness beacon via the [Proof-of-Time (PoT)](proof-of-time.md) chain, which serves as a global 'clock' for the network where the current 'time' is the height of the PoT chain. It also provides the source of randomness for block production.
4. **First Segment Archiving**: The data attached to the genesis block triggers the [archiving](proof-of-archival-storage/archiving.md) of the first segment of the canonical history of the chain. It produces the first 256 pieces and announces them to the [DSN](../distributed-storage-network.md).
5. **History Seeding**: The Autonomys Labs team uploads an initial archive of useful seed data, including the whitepaper, archived data from previous testnets, and community-nominated submissions, to the network.
6. **Initial Plotting**: [Farmers](../nodes.md) create their plots from the newly archived pieces. As soon as [plotting](proof-of-archival-storage/plotting.md) is complete, they can start [farming](proof-of-archival-storage/farming.md) blocks.
7. **Block Production**: Although block production begins, [$AI3 farming rewards](../rewards-and-fees/) are not issued until the Space Race is complete. Meanwhile, full nodes start syncing the chain and participating in consensus.
8. **Space Race**: The [Space Race](https://www.autonomys.xyz/post/announcing-the-autonomys-mainnet-launch-space-race) is a collaborative effort between farmers to reach a set goal of pledged space that will automatically enable block and vote rewards. It ensures a safe cold start for the network during which we can bootstrap its [security](security.md).
9. **$AI3 Rewards Enabled**: After the Space Race's conclusion, block and vote rewards are issued to farmers who successfully audit their plots for a block or vote-eligible solution. Rewards decrease over time according to our [dynamic token issuance schedule](https://www.autonomys.xyz/post/from-space-race-to-long-tail-crafting-a-sustainable-token-issuance-model-for-a-resilient-autonomys-network).
