---
description: The third phase of the Subspace Protocol
---

# Farming

**Farming** involves solving block challenges based on previously created plots in order to participate in consensus.

Plot audits are designed to be SSD-friendly, favoring a random read approach over large sequential reads, and optimized for typical SSD read size. For illustration, a farmer only needs to read below 32KiB at a random location per sector to check for a solution, and they only need to read more if their solution is eligible to win the block.

## Background

The difficulty of farming is defined by the solution range: the narrower the solution range, the fewer possible chunks exist within that range, the smaller the probability for any given farmer to be storing such chunks on their disks. Similarly to Bitcoin, the Subspace Protocol uses an automatic difficulty adjustment mechanism to address fluctuations in network storage and keep block times relatively stable. The Autonomys Network currently targets a block time of approximately 6 seconds. The difficulty is adjusted every 2016 blocks based on the actual time it took to farm the previous 2016 blocks.

<figure><img src="../../../.gitbook/assets/infographic_farming.png" alt=""><figcaption><p>Farming</p></figcaption></figure>

## Workflow

After a farmer has [plotted](plotting.md) at least one sector, they can begin farming. As soon as they observe a new challenge from the global randomness beacon, farmers scan each plot sector for a solution and propose a block if they find one, as follows:

1. For each sector, derive a corresponding audit index.
2. Read from disk the s-bucket at that index.
3. Scan it for a chunk within the acceptable solution range from the block challenge.

As each bucket contains chunks from all records, if a farmer honestly stores all encoded records in the sector, they have the highest chance of success.

If a farmer finds a winning chunk for the current block challenge, they perform the following steps to prove their solution is valid:

1. Identify the parent record of the winning chunk from its offset in the s-bucket.
2. Read from disk all other encoded chunks of this record.
3. Compute the corresponding proof-of-space table the same way as during plotting.
4. Query the table for proof values.
5. Decode the record by XORing it with those proofs.
6. Compute a KZG witness that the winning chunk belongs to a piece in the archived history.

Finally, the farmer can propose a block with the attached solution and proof of a valid solution.
