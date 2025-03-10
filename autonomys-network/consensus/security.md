---
description: An overview of Subspace Protocol security
---

# Security

As a complex system, the Autonomys Network has several potential attack vectors—some are general blockchain-related vulnerabilities, while others target Proof-of-Capacity (PoC)/Proof-of-Archival-Storage (PoAS) consensus chains specifically. The Subspace Protocol addresses these attack vectors via a number of mechanisms. For a detailed security analysis, refer to our paper '[_Dilithium: A Proof-of-Archival-Storage Consensus Protocol for Subspace_](https://github.com/subspace/consensus-v2-research-paper)'.

## Security against general blockchain attacks

### Grinding on block challenges

To prevent grinding on block challenges, the Subspace Protocol draws unique, unpredictable challenges using the [Proof-of-Time (PoT)](proof-of-time.md) chain.

In PoW-based blockchains, block challenges come from the previous full block. PoC/PoAS-based blockchains cannot follow this approach, as changing the block content does not affect proof-of-space validity.

Progression on the Autonomys Network consensus chain is instead based on 'time slots', each associated with a run of the PoT algorithm, the output of which is used to draw the block challenge for that slot. By design, grinding on PoT is extremely hard.

### Costless simulation attacks

To mitigate against costless simulation attacks, where attackers are able to create an outsized number of blocks in proportion to their pledged disk space, the Subspace Protocol implements correlated randomness in block challenges.

Using the c-correlation method, where challenges for 'c' blocks are correlated and deterministic, an attacker attempting to simulate many potential forks gains significantly less power, as the ability to maneuver across these forks becomes increasingly limited as 'c' becomes larger.

### Bribing attacks

To prevent potential issues like bribing attacks that arise with the correlation of block challenges, and the predictability window associated with c-correlation in general, the Subspace Protocol uses PoT outputs to draw block challenges.

This means block challenges are not known in advance and only revealed when the timeslot arrives, even though the challenges for 'c' blocks are deterministic.

### Long-range attacks

To prevent long-range attacks, the Subspace Protocol integrates PoT as a fundamental component.

This means that an attacker attempting to bootstrap a competing and longer (i.e. heavier) chain cannot do so without cost, as they must show that sufficient time has passed for the lifespan of this fork. In other words, as in PoW, an attacker needs to spend an infeasible amount of sequential work to maintain an attack.

## Security against PoC/PoAS attacks

### Time-memory algorithms (plot compression)

To prevent attacks on PoAS consensus, the Subspace Protocol applies a masking function during farmers' plot creation.

This function—described in '[_Beyond Hellman's Time-Memory Trade-Offs with Applications to Proofs of Space_](https://eprint.iacr.org/2017/893)'—is designed such that the gain in trading computation (time) over storage (memory) is very small.

### On-the-fly plotting

To prevent farmers from creating plots on the fly after seeing a challenge, the Subspace Protocol is designed with two properties in mind:

1. The masking function is memory-hard. This means that creating a plot is constrained by the amount of memory the farmer has, as well as the rate of the memory IO operations it can perform.
2. Creating plots on-demand is uneconomical, and thus irrational. Due to the different resource requirements of running the masking function, the cost of running it to simulate a sufficiently large amount of storage is significantly higher than the cost of purchasing the same amount of storage, plotting it, and maintaining a farmer. In other words, a rational farmer willing to spend the cost for on-demand plotting is better off spending this cost on 'real' plotting.
