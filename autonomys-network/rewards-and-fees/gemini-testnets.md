---
description: An overview of dynamic token issuance on Autonomys' Gemini testnets
---

# Gemini Testnets

On Autonomys' Gemini testnets, farmers initially received 0.1 $tSSC in block rewards for the blocks they proposed, and 0.1 $tSSC for the votes they submitted. The decay function reduced rewards every block as the chain progressed following the exponential decay function:

$$
reference\_subsidy = initial\_subsidy * e^{-initial\_subsidy*(n-decay\_block\_start)/max\_issuance\_tokens}
$$

Both block proposer rewards and vote rewards were computed using the same formula.

Dynamic issuance was tested on the Gemini 3h testnet where:

* $$initial\_subsidy = 0.1$$ $tSSC per block
* $$n$$ is the current block height
* $$decay\_block\_start = 718959$$ (the block when the decay function was activated)
* $$max\_issuance\_tokens = 100000000$$ $tSSC

On Gemini-3h, the reference subsidy issuance decayed roughly following the curve below, starting at 0.1 $tSSC per (empty) block, and decreasing over the next 1,296,000 blocks (\~90 days).

<figure><picture><source srcset="../../.gitbook/assets/issuance-decay-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../.gitbook/assets/issuance-decay-light.svg" alt=""></picture><figcaption><p>Dynamic reward issuance on Gemini-3h</p></figcaption></figure>

Block proposer rewards were also dynamic based on the demand for blockspace, with the protocol decreasing proposer rewards in response to increased execution fees earned by proposers (due to blockspace utilization). Blockspace demand was measured as an exponential moving average of the percentage of the maximum blockspace used by normal transactions over the last 100 blocks (excluding operational transactions like votes and fraud proofs):

$$
blockspace\_utilization = \sum_{\mathclap{}}encoded\_transaction\_size / 3.75 MiB
$$

The final formula for block proposer rewards was:

$$proposer\_reward = reference\_subsidy - min(reference\_subsidy, max\_block\_fees) * blockspace\_utilization$$

Vote rewards represented 90% of the reference subsidy, and were unaffected by utilization:

$$voter\ reward = 0.9 * reference\_subsidy$$

The remaining 10% of each vote reward was received by the proposer of the block that included the vote to incentivize the proposer to include votes.
