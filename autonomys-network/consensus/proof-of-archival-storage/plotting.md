---
description: The second phase of the Subspace Protocol
---

# Plotting

**Plotting** is the process of creating and maintaining plots on a disk, during which pieces are gathered and organized into plots of several sectors.

Each sector contains an encoded replica of a uniformly random sample of pieces across all archived history. This sampling ensures that the data is distributed among farmers proportionally to their pledged disk space and replicated evenly.

Plotting is based on two core ideas:

* Erasure coding helps protect the data against loss in the event of failures and network partitions.
* Memory-bandwidth-bound encoding provides a more cost-effective and eco-friendly alternative to proofs-of-work, while providing provable time/memory trade-offs and security guarantees.

Combining these two ideas allows us to create unique, provable replicas for each farmer that are difficult to fake with computation or to compress. This scheme also makes scanning and verifying the plots easier, ensuring the chain history data is recoverable. Our memory-bandwidth-bound encoding construction is inspired by the [Chia](https://www.chia.net/) protocol paper '[_Beyond Hellman's Time-Memory Trade-Offs with Applications to Proofs of Space_](https://www.semanticscholar.org/paper/Beyond-Hellman's-Time-Memory-Trade-Offs-with-to-of-Abusalah-Alwen/39e70d67eeb5ce140171f6d0629daec3b54d74f3)**'**. The Subspace Protocol adopts a custom implementation of the Chia Proof-of-Space (PoS) plotting function as a memory-bandwidth-bound function to encode, or 'mask', the pieces in farmer plots.

## Background

In short, the PoS plotter generates a table of permuted outputs from a set of random functions. The table size is determined by a memory bandwidth requirement parameter _k_ set to 20, and the random functions are determined by a _seed_. When challenged at an _index_, the table outputs a short _proof-of-space_ that can be efficiently verified. We do not use the proof-of-space directly to verify that a farmer has pledged a certain amount of space, as Chia does. Instead, we use it to prove that a farmer utilized the required memory bandwidth for encoding the plot.

<figure><picture><source srcset="../../../.gitbook/assets/PoS_Table-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../../.gitbook/assets/image (15).png" alt=""></picture><figcaption><p>PoS Table</p></figcaption></figure>

## Workflow

A plot can cover an entire disk or span across multiple disks, and there is no limit to the amount of storage a farmer can pledge to the network. Plots consist of equally-sized sectors (around 1 GiB each). Each sector is a pseudorandom selection of 1,000 pieces, uniformly sampled throughout the history up to that point. For example, if the farmer creates a new sector when the history consists of 50,000 pieces (50 GiB), the 1,000 pieces for this sector will be a uniform selection from the existing 50,000 pieces. In addition, the farmer must save the current history size, as it will determine when the sector will need to be updated with newer pieces.

<figure><picture><source srcset="../../../.gitbook/assets/Raw_Sector-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../../.gitbook/assets/image (16).png" alt=""></picture><figcaption></figcaption></figure>

Once a farmer has obtained all 1,000 pieces for a sector from the network, they create an encoded replica. Only the piece’s historical data (the record) is encoded. The KZG commitment and witness included in a piece are saved separately in the sector metadata as they will be needed later for farming.

For each record, the plotting algorithm performs the following steps in memory:

1. Erasure code (extend) the record data by interpolating a polynomial over chunks of the record.
2. Derive a unique pseudorandom and verifiable _seed_.
3. Based on this _seed_, generate a proof-of-space table using memory bandwidth resources set by the global protocol memory requirement parameter _k_. This memory-intensive computation prevents malicious farmers from creating replicas after the new block challenge is announced, making it more rational for them to store the replica rather than try to compute it on the fly every time.
4. Query the generated table for enough ($$2^{15}$$) proof-of-space values to mask every chunk of the record.

<figure><picture><source srcset="../../../.gitbook/assets/PoS_Lookup-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../../.gitbook/assets/image (17).png" alt=""></picture><figcaption></figcaption></figure>

5. Encode each extended record chunk by XOR-masking it with the corresponding proof-of-space value.

<figure><picture><source srcset="../../../.gitbook/assets/Piece_Encoding-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../../.gitbook/assets/image (18).png" alt=""></picture><figcaption></figcaption></figure>

After all records in the sector have been encoded as described, the farmer spreads them into s-buckets chunk-wise. Ultimately, each bucket will contain chunks from all records. The first bucket will have the first chunks of each record; the second bucket will have the second chunks, and so on. The s-buckets are then written to disk, and the plotting process of the sector is complete in a single write operation.

<figure><picture><source srcset="../../../.gitbook/assets/Encoded_Sector-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../../.gitbook/assets/image (19).png" alt=""></picture><figcaption></figcaption></figure>

Each bucket represents a potential winning ticket in the block proposer lottery. For each challenge, a farmer will scan one s-bucket (containing one chunk of each record they store in a sector) to check whether any of them are eligible to win a block. As a result, a farmer has a unique encoded replica that is difficult to compress or compute on demand. An economically rational farmer is incentivized to store as many honestly encoded replicas as possible to maximize their chances of winning a block.

## Replotting

As the chain grows, we need to ensure that new data is replicated as much as older data in the blockchain history. To keep this replication factor constant, farmers must periodically update their plots by replotting expired sectors with a new selection of pieces.

The expiry point for a sector is determined by the history size at the time the farmer initially plotted the sector, and is randomly assigned to occur sometime before the history size quadruples (i.e., if a farmer plotted a sector when the history size was 50 GiB, the expiry point will occur before the history reaches 200 GiB). When a sector reaches its expiry point, the block proposer challenge solutions coming from this sector will no longer be accepted by other peers, incentivizing the farmer to update their plot. When replotting, farmers erase the expired sector and repeat the plotting process anew, replicating a fresh history sample. Each replotting creates a new sector in memory and saves it to disk in a single write operation.

<figure><picture><source srcset="../../../.gitbook/assets/Replotting-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../../.gitbook/assets/image (20).png" alt=""></picture><figcaption></figcaption></figure>

In a plot spanning multiple GBs, sectors will be updated randomly, one at a time, so replotting is amortized over a long period, meaning a farmer never needs to erase and re-create their whole plot and miss out on challenges. The plot refreshing will be practically invisible to the farmer and allow their uninterrupted participation in consensus. The bigger the chain grows, and the longer the farmer participates in the network, the less frequent the replotting on their disks will be.

After [genesis](../genesis.md), the network was seeded with 20 GiB of history, meaning farmers who joined after the seeding started plotting with an initial history size of 160 segments. Assuming a 1 TB SSD plot, a farmer would thus need to replot 3.5 TB of data on average by the time the chain history reaches 1TB in size, 6.2 TB of data by the time history reaches 10 TiB, and 8 TB by the time history reaches 50 TiB. Given the common TBW (Total Bytes Written) for consumer grade 1 TB SSDs of 300-600 TB, Autonomys farming requires under 3% of the SSD's total endurance to farm over several years (for comparison, Ethereum's full chain data size is \~21 TiB as of February 2025 via [Etherscan](https://etherscan.io/chartsync/chainarchive)).

<figure><picture><source srcset="../../../.gitbook/assets/Replottingby10TiB-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../../.gitbook/assets/image (21).png" alt=""></picture><figcaption><p>Average TB replotted on a 1 TB SSD from genesis to 10 TiB (40,960 archived segments)—the increase in the amount of data replotted slows as the chain grows</p></figcaption></figure>

The next and final phase of Subspace Protocol consensus is [farming](farming.md).
