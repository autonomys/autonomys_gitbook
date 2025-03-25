---
description: An overview of the Proof-of-Time (PoT) chain and randomness beacon
---

# Proof-of-Time (PoT)

## Overview

A vulnerability of pure proof-of-stake (PoS) (and by extension proof-of-capacity (PoC)) systems lies in their susceptibility to [long-range attacks](https://doi.org/10.48550/arXiv.1910.02218). Unlike proof-of-work (PoW) systems, where block production is physically constrained by computational power, PoS/PoC systems lack this inherent limitation. In PoW, the resource is expended directly to produce a block, and only once, while in PoC the disk space “resource” is not tied to a specific block and only provides the eligibility to produce a block, reused over many blocks. Consequently, an adversary with sufficient resources could potentially rewrite a significant portion of the blockchain at any point in the chain’s history, compromising its immutability and security. This vulnerability stems from the fact that historical stake distributions can be manipulated without incurring the substantial energy costs associated with PoW systems.

Additionally, PoS/PoC systems often struggle to achieve the [dynamic availability and unpredictability inherent in PoW systems](https://doi.org/10.48550/arXiv.2010.08154). The challenge lies in creating a system that can adapt to fluctuating participation rates while ensuring that block proposers remain unpredictable, thus preventing targeted attacks or manipulation. These properties are crucial for maintaining robust network operation and [security](security.md) against various attack vectors.

The Autonomys Network addresses these challenges by implementing a separate proof-of-time (PoT) chain that interlinks with the [PoAS chain](proof-of-archival-storage/). This design prevents longrange attacks by enforcing a verifiable time constraint between block proposals, analogous to the [arrow of time](https://doi.org/10.48550/arXiv.2010.08154) in PoW systems. PoT guarantees that a certain amount of wall-clock time must elapse between block proposals, preventing an adversary from rewriting history by “going back in time.” PoT is constrained physically, similar to PoW, but is not parallelizable (technically, it is proof of _sequential_ work), and an attacker cannot immediately generate a successful multi-year retroactive fork even with faster hardware.

The elapsed time guarantee is achieved by iterative evaluation of an inherently sequential delay function. The choice of delay function is crucial to the security and efficiency of the PoT system. After extensive analysis of existing verifiable delay functions (VDFs), we chose to employ repeated [AES-128 encryption](#user-content-fn-1)[^1]. This decision balances security, efficiency and resistance to hardware acceleration. Using the Advanced Encryption Standard (AES) leverages its extensive cryptographic research history and the availability of hardware acceleration in modern CPUs, making it an optimal choice for this application. Based on a joint study with hardware-accelerated cryptography lab Supranational, we do not expect a significant speedup over the best AES implementation, even with an ASIC.

To maintain the PoT chain, the network introduces a new node role called [_timekeepers_](../nodes.md). These nodes are responsible for evaluating the delay function and disseminating outputs. To provide PoT evaluation, timekeepers require the highest-end CPUs—unavailable to most farmer nodes. Delegating timekeeping to a separate class of nodes ensures decentralization on the consensus level, while maintaining protocol security with minimal honest participation, where the presence of at least one honest timekeeper is sufficient.

To achieve asymmetric verification time for the AES-based delay function, timekeepers publish a set of intermediate checkpoints—currently 8, spaced uniformly—alongside the output. Farmers can validate each checkpoint independently and in parallel to reduce overall verification time. Including checkpoints allows other nodes to validate the output ≈ 7 times faster and use ≈ 4 times less power than evaluation by leveraging instruction-level parallelism.

<figure><img src="../../.gitbook/assets/infographic-proof-of-time (1).png" alt=""><figcaption><p>Proof of Time checkpoints</p></figcaption></figure>

The [Subspace consensus protocol](./) utilizes a [farming](proof-of-archival-storage/farming.md) dynamic that mimics the random nature of Bitcoin’s mining dynamic, while only expending a small amount of electricity. This is achieved through PoT-based block challenges for the block proposal lottery, based on _'_[_PoSAT: Proof-of-Work Availability and Unpredictability, without the Work_](https://doi.org/10.48550/arXiv.2010.08154)_'_. The PoT chain serves as a randomness beacon, providing unpredictable and verifiable inputs for block challenges, thus addressing the issue of long predictability windows often seen in protocols using generic verifiable random functions. This unpredictability is at the same level as that of PoW protocols and is stronger than those using verifiable random functions.

The security of the PoT system is further enhanced by several key mechanisms. Sequentiality is achieved through output chaining between slots, ensuring that each new output depends on the previous one. To compensate for network delays, the system implements a tunable lag parameter, allowing sufficient time for propagation and verification of PoT outputs before block proposals. The Autonomys Network also incorporates measures to mitigate the potential advantage of faster timekeepers, including periodic entropy injection. To prevent manipulation of randomness, the network employs an injection mechanism similar to that used in [Ouroboros Praos](https://ia.cr/2017/573). This approach prevents attackers from controlling slot challenges by strategically releasing or withholding blocks, further enhancing the unpredictability and security of the system.

## Design challenges

### Long-range attacks

Unlike in PoW, the process of block production in PoS and PoC-based blockchains is not physically constrained. This makes these protocols vulnerable to _long-range attacks_, where an attacker can very quickly produce an alternative chain all the way to the current time that can potentially be longer than the current canonical chain.

<figure><picture><source srcset="../../.gitbook/assets/Long_Range_Attack-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/image (28).png" alt=""></picture><figcaption><p>Long-range attack</p></figcaption></figure>

To perform a long-range attack, an adversary needs to control enough resources at some point in the chain's life to rewrite a significant portion of the chain history. In PoW protocols like Bitcoin, this requires controlling over 50% of the total network hashrate for a sustained period of time. Long-range attacks are thus infeasible in practice as it takes a long time to mine an alternative chain from the past, enforcing an arrow of time. This property is key to tolerating fully dynamic honest and adversarial participation. However, long-range attacks remain a serious threat to non-PoW-based consensus protocols, including PoC (and PoS), for example:

Suppose that in the first year of a blockchain's operation, all farmers were honest and collectively pledged 100 TB of storage. Suppose by the second year, the total storage pledged has reached 1 PB, out of which an adversary has dedicated 200 TB. Although at no point does an adversary control more than 20% of storage, using their 200 TB, the adversary could rewrite the chain history back to genesis by participating in all past lotteries to win blocks, and then grow a chain instantaneously from genesis to surpass the current longest chain. This is possible because the adversary's resources are significant enough to win a disproportionately large number of past lotteries relative to their share of total storage. Such a long-range rewrite seriously threatens the security and immutability of the chain history.

### Dynamic availability and unpredictability

Alternative consensus protocols like PoS and PoC strive to replicate the dynamic availability and unpredictability of PoW. Dynamic availability refers to the capacity of a blockchain network to maintain robust operation in environments where nodes may join or leave dynamically, while unpredictability refers to the inability of any node to predict the next block proposer. These properties are important for the security and liveness of the network.

Permissionless PoW remains the most robust method for achieving consistent availability and unpredictability in a decentralized system (evidenced by Bitcoin's continuous availability for over a decade despite a constantly varying hashrate due to miners joining and leaving the network). Protocols using generic verifiable random functions to elect block proposers usually do not achieve unpredictability at the same level, and may suffer from a long predictability window of block challenges.

## Autonomys' solution

The Autonomys Network utilizes a proof-of-time (PoT) chain interconnected with the PoAS consensus chain to prevent long-range attacks and achieve dynamic availability and unpredictability. This is based on the paper [PoSAT: Proof-of-Work Availability and Unpredictability, without the Work](https://arxiv.org/abs/2010.08154) by Soubhik Deb, Sreeram Kannan and David Tse.

The PoT chain addresses long-range attacks by enforcing an arrow of time similar to PoW, guaranteeing that a certain amount of wall-clock time must elapse between block proposals, thus preventing an adversary from rewriting history by "going back in time". Similar to PoW, PoT is constrained physically, however, it is not parallelizable (as its technically proof-of-_sequential-_&#x77;ork), preventing an attacker from immediately generating a years-long fork even with faster hardware.

The elapsed time guarantee is achieved by iterative evaluation of an inherently sequential function. The output of such a function is unpredictable and is used to build a randomness beacon for block challenges. The PoT-based randomness beacon guarantees that block challenges, and hence block proposers, are not predictable, and is stronger than using verifiable random functions. This allows PoAS-based farming to achieve the same unpredictability as PoW-based mining, while using only a fraction of the electricity, ensuring fairness for all participants.

### Timekeeping

[Timekeeper nodes](../nodes.md) maintain the PoT chain, evaluating the delay function, and announcing the outputs to other nodes. A single honest timekeeper is sufficient for the security of the protocol, but there should ideally be multiple timekeepers running concurrently for robustness and decentralization. Although running a timekeeper is currently unincentivized, independent timekeeping contributes to stable block production, which benefits all network participants.

Farmers and operators can also be timekeepers, however, operators are better suited to timekeeping as they already possess the necessary powerful hardware. Timekeeping fully consumes a dedicated CPU core, and should thus be run on a separate last generation machine with no other processes. This setup allows for optimal performance and secures the protocol against malicious timekeepers.

The genesis of the PoT chain was concurrent with the [genesis](genesis.md) of the PoAS consensus chain. The input to the first slot was a random seed publicly announced at launch to ensure equal opportunity. For each subsequent slot, the output of the previous slot serves as the input. By chaining the outputs, the timekeepers enforce sequentiality and prevent skipping ahead in time.

### Randomness beacon

The Subspace Protocol uses the sequence of random values provided by PoT evaluation as a source of randomness—or randomness beacon—for consensus block challenges. As Autonomys targets one block challenge per second, we set the delay function evaluation to output a proof every second. For every time slot, timekeepers evaluate the delay function for a set number of iterations to generate fresh global randomness before announcing the output to the network. This is then used by farmers to determine the next block proposer.

<figure><picture><source srcset="../../.gitbook/assets/PoT_Challenges-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/image (30).png" alt=""></picture><figcaption></figcaption></figure>

Farmers receive and verify these outputs before scanning their plots for any chunks of history close enough to the challenge threshold to claim the block. If they have stored the correct chunks, the farmer provides a proof-of-space for them, proposes the block, and earns rewards. The randomness is revealed a few slots in advance to ensure every farmer on the network has enough time to receive it, scan their plots, and submit their proof-of-space (if they win). Farmers' inclusion of PoT outputs in block headers integrates the PoT chain with the PoAS consensus chain.

Every 50 blocks, entropy from the consensus chain is injected back into the PoT chain by using the farming solution and PoT output from a deep consensus block header as the new input for the delay function. Injection prevents an adversary from simulating a consensus chain fork without also simulating a PoT chain fork. Forks in the consensus chain will result in a different sequence of PoT outputs, hence, an attacker that forks the chain at some historical point will have to also physically run the PoT algorithm.

### AES-based delay functions

The Autonomys Network uses repeated AES-128 encryption as an alternative to existing verifiable delay functions (VDFs), such as repeated squaring in groups of unknown order, as AES fulfills our requirements of being iterative and non-parallelizable, and producing a short, random, verifiable output.

AES was chosen following an extensive study of existing VDF constructions owing to its research maturity and extremely efficient hardware and software implementation using hardware acceleration instructions. Based on a joint study with [Supranational](http://supranational.net/), we do not expect a significant speedup over the best AES implementation, even with an ASIC.

Timekeepers publish a set of intermediate checkpoints—currently 8, spaced uniformly—alongside their output to achieve asymmetric verification time for the AES-based delay function. Farmers can validate each checkpoint independently and in parallel to reduce overall verification time. Including checkpoints allows other nodes to validate the output \~7 times faster and use \~4 times less power than evaluation by leveraging instruction-level parallelism.

The target number of iterations is currently set to \~183 million with the aim of achieving approximately 1 second per time slot on high-end CPUs. Autonomys will continuously monitor hardware capabilities and adjust the target to maintain approximately 1 second slots as needed. It is crucial to benchmark the delay function on the best available hardware to ensure that no one can gain an advantage by evaluating the delay function faster than others to predict future randomness outputs.

### Security

The security claim for the PoT chain:

As long as there is at least one honest timekeeper online at all times, and network delay is bounded, all honest nodes can determine the correct PoT output, and hence the correct slot challenge.

This is achieved by carefully implementing or accounting for:

1. **Sequentiality**: The randomness beacon achieves sequentiality by chaining slot outputs, where each output is used as an input to the delay function for the next slot.
2. **Network delay**: Farmers receiving PoT outputs for challenges immediately start auditing their plots (and proving if they have a winning solution), but can only submit the solution after 𝑟 slots. This lag parameter 𝑟 is currently set to 4 slots to ensure there is enough time to propagate, verify the PoT output, and prove a solution on common farmer hardware. Increasing 𝑟 grants an honest node more time to solve challenges, but also allows a malicious node more time to attempt to plot on-the-fly.
3.  **Faster timekeepers**: The Autonomys Network addresses the potential risk of an attacker running a timekeeper node on hardware faster than all other timekeepers via several mechanisms:

    1. Speed gains are not cumulative over time: because of entropy injection every 50 blocks (\~5 min), the attacker's advantage is reset.
    2. If a faster timekeeper gossips their PoT to the network, other timekeepers will continuously sync to catch up to them. If a faster timekeeper withholds PoT, only using it to produce blocks on their own, although they do have some prediction window (depending how much faster they are), they either need a significant percentage of the network's disk storage or to attempt on-the-fly plotting, both of which are near-impossible (as described in [Security](security.md)). A faster PoT also makes long-range attacks more feasible, but an attacker is still subject to the above restrictions.

    We will continuously monitor the rate of PoT progression in comparison to real wall-clock time to detect for any faster timekeepers.
4. **Difficulty adjustments**: The iteration count for the PoT delay function is benchmarked to be as close to real wall-clock time as possible. With improvements in hardware, faster honest timekeepers can be deployed and the iteration count increased to account for this.
5. **Predictability**: Attackers can only predict slot challenges in advance if they have a faster timekeeper, and even then, they only last until the next injection.
6. **Biasing randomness**: Attackers cannot control the slot challenges of the next time interval by releasing or withholding their blocks from the current interval via the injection mechanism (see [Ouroboros Praos](https://eprint.iacr.org/2017/573.pdf) for a security proof).

[^1]: While AES is not technically a VDF, as encryption (proving) and decryption (verification) take the same number of CPU cycles, it can be used as a VDF in practice by parallelizing verification.
