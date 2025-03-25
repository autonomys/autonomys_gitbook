---
description: Autonomys's Proof-of-Archival-Storage (PoAS)-based consensus layer
---

# Subspace Protocol (PoAS Consensus)

The Autonomys Network is an instance of the Subspace Protocol—a unique, lightweight, [secure](security.md) Proof-of-Archival-Storage (PoAS) consensus and data availability mechanism. The Subspace Protocol ensures there is a single source of truth for the blockchain's state and history across all nodes participating in the network. Based on storing pieces of the chain history in allocated disk space, rather than compute power or staked assets, PoAS consensus is eco-friendly, permissionless and fair, remaining accessible to anyone with an SSD—a widely distributed commodity.

To participate in a Proof-of-Archival-Storage, [farmers](../../auto-suite/spaceacres-cli/farmers.md) first create and store as many provably unique partial replicas of the chain history as their allocated disk space allows, before responding to random, publicly verifiable storage audits, which allow them to forge new blocks. This stands in contrast to the Proof-of-Capacity (PoC) protocols proposed by [Spacemint](https://ia.cr/2015/528), [Chia](https://chia.net/wp-content/uploads/2022/07/ChiaGreenPaper.pdf), and [SpaceMesh](https://eprint.iacr.org/2016/035.pdf), in which nodes store randomly generated data, rather than useful files. In incentivizing the storage of the blockchain's history, PoAS also resolves the key mechanism design failure that has hindered the scalability of PoC chains like Filecoin and Chia and led to their centralization.&#x20;

PoAS—inspired by Sergio Lerner’s [Proof-of-Unique-Blockchain-Storage](https://bitslog.com/2014/11/03/proof-of-local-blockchain-storage/) mechanism (but utilized directly for consensus)—combines the high security of Bitcoin-style Proof-of-Work (PoW) with the energy-efficiency of Ethereum-style Proof-of-Stake (PoS). The Subspace Protocol was built to provide a superior user experience (UX) to existing PoC protocols, while maintaining the highest level of consensus security. Its most relevant UX and performance metrics are:

* _Setup time:_ hours–days (depending on allocated disk space)
* _Proof-generation time:_ < 1 second
* _Proof size:_ < 1 KB
* _Verification time:_ 0.001–0.01 seconds

The latest iteration of the [Subspace Protocol](https://github.com/subspace/consensus-v2-research-paper/blob/main/consensus) uniquely combines [KZG polynomial commitment](https://cacr.uwaterloo.ca/techreports/2010/cacr2010-10.pdf), [erasure coding](https://iqua.ece.toronto.edu/papers/junli-survey13.pdf), and [function inverting](https://ia.cr/2017/893) to address outstanding design challenges, significantly improving upon [previous versions of the protocol](https://cdn.prod.website-files.com/61526a2af87a54e565b0ae92/617759c00edd0e3bd279aa29). Read the [Dilithium research paper](http://github.com/subspace/consensus-v2-research-paper/blob/main/consensus_v2.pdf) for a more detailed description of our revised consensus design, and our [original Subspace whitepaper](https://gateway.autonomys.xyz/file/bafkr6ibscehgtz4l5ee6rb3tnofcceaztqympdw6k5b6efkoe77uswvoqy) for a full explanation of its fundamental ideas.

## Contents

Read the following subsections for technical details of the Subspace Protocol consensus mechanism:

1. [**Genesis**](genesis.md)
2. [**Data Flow**](data-flow.md)
3. [**Proof-of-Archival-Storage (PoAS)**](proof-of-archival-storage/)
   1. [**Archiving**](proof-of-archival-storage/archiving.md)
   2. [**Plotting**](proof-of-archival-storage/plotting.md)
   3. [**Farming**](proof-of-archival-storage/farming.md)
4. [**Proof-of-Time (PoT)**](proof-of-time.md)&#x20;
5. [**Security**](security.md)

## Technical Overview

PoAS is a three-phase protocol, consisting of:

* [**Archiving**](proof-of-archival-storage/archiving.md)**:** a recurring deterministic phase completed by all farmer nodes as the blockchain expands.&#x20;
* [**Plotting**](proof-of-archival-storage/plotting.md)**:** a unique setup phase completed individually by each farmer node.
* [**Farming**](proof-of-archival-storage/farming.md)**:** a probabilistic audit phase based on a recurring slot challenge from a secure randomness beacon with a frequency of one challenge per second.

<figure><picture><source srcset="../../.gitbook/assets/Consensus_Phases-dark (1).svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/image (6).png" alt=""></picture><figcaption></figcaption></figure>

A key design challenge is how to ensure the uniqueness of each farmers' plot. As the blockchain's history is not unique to any one farmer, farmers cannot simply store the raw chain history, otherwise dishonest farmers could share a single copy of the chain history to emulate an unlimited amount of disk space. PoAS solves this as follows:

### [Archiving](./#archiving)

Before plotting, farmers must prepare the raw blockchain history for compatibility with the Subspace plotting protocol by archiving. Archiving applies error-correction coding—specifically the Reed-Solomon code—to guarantee that even if a piece of data (a collection of blocks) is not stored by any farmer, it can be recovered by other pieces. The replication factor used is 1/2, meaning half the network's storage is dedicated specifically to implementing this error-correction technique. This is much more efficient for recovery purposes than using this space to store each block twice. Archiving also utilizes KZG polynomial commitment—a type of cryptographic commitment scheme—to facilitate the later farming phase, during which farmers prove that they stored a certain piece of chain history.

### [Plotting](proof-of-archival-storage/plotting.md)

During plotting, farmers create their own unique plots in two steps:

1. A deterministic algorithm (involving the farmer's ID, the current blockchain height, and other factors) picks pieces of the blockchain history for the farmer to store on their disk. This ensures—with high probability—that pieces are allocated uniformly at random, and therefore that no piece of history will be missing.
2. A deterministic algorithm (involving the farmer ID and piece of history) 'masks' the farmer's assigned pieces with unique, verifiable 'masking data'. Masking involves producing a string of bits that are XOR-ed with the bit representation of the selected piece of history. This ensures different farmers obtain different masking data for the same piece and each plot contains unique pieces of data, meaning dishonest farmers cannot share the same raw history. Autonomys adopts Chia's cryptographic protocol as it demands both time and electricity for generation, preventing dishonest farmers from attempting to produce the masking data on the fly and re-using their raw data for several plots.

### [Farming](proof-of-archival-storage/farming.md)

Once a farmer has created their plot, they can start farming it. Farming is similar to mining in other blockchains, where block challenges are drawn and miners (farmers) attempt to produce a block with their resources (stored pieces of chain history). Block challenges are drawn from a secure randomness beacon which updates every second. The randomness is obtained from an AES-based [Proof-of-Time (PoT)](proof-of-time.md) component anchored to the blockchain history itself. In order to win a block challenge and produce a block, a farmer must submit a proof including both the raw piece of chain history and its masking data. As the masking data is verifiable, anyone can check that it was the unique masking data for that specific piece of history and farmer ID.
