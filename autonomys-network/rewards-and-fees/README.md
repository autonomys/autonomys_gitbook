---
description: An overview of the $AI3 token and its structure for rewards and fees
---

# $AI3 Rewards & Fees

## **Introduction**

**$AI3** _(formerly SSC/ATC)_ is the native token used for transactions and staking on the Autonomys Network ($tAI3 on our Taurus testnet)_._

## Rewards & fees

All participants in the Autonomys Network are compensated fairly for their maintaining the network via:

* **Fees**: For transactions on the Autonomys Network (by users sending transactions)
* **Rewards**: For participants' work on the Autonomys Network (via the protocol's issuance of newly minted $AI3)

Different participants receive their compensation through a combination of fees and rewards depending on their role.

### Farmers

Farmers pledge SSD space to the network and receive $AI3 in the form of:

* _fees_ for the transactions and bundles they include in consensus chain blocks
* _block rewards_ for the blocks they propose (issued by the protocol)
* _vote rewards_ (issued by the protocol)

### Operators

Operators pledge compute and a minimum stake to the network and receive $AI3 in the form of:

* _fees_ for the [domain](../decoupled-execution/domains/) transactions/bundles they produce, validate and execute (via a nomination tax)

The nomination tax is a commission collected by operators on nominator $AI3 fees before they are proportionally distributed to the nominators staked to that operator. Operators receive the fees for their executed transactions once the relevant domain block has cleared the challenge period. Domain transactions (e.g. EVM contract calls) are usually significantly more computationally intensive than consensus chain transactions (e.g. balance transfers), and are therefore more expensive in order to compensate operators fairly. For more details, see [domain block fees](../decoupled-execution/domains/#domain-block-fees).

### Nominators

Nominators pledge a minimum stake to an operator's nomination pool and receive $AI3 in the form of:

* a share of the operator's _fees_ for increasing the size of their pool (based on the nominator's share of the pool)

$AI3 holders nominate stake to operators to increase their chances of executing and processing blocks. The larger the nomination pool, the higher the probability of producing a bundle and receiving the associated fees. Operators are thus motivated to attract as many nominators as possible to increase the size of their nomination pool. For more details on pool shares and fee calculations, see [nomination pools](../decoupled-execution/staking.md#nomination-pools).

## Transaction fees

Every transaction on the Autonomys Network has a:

* **Length**: The number of bytes it consumes on the network
* **Weight**: The number of picoseconds it takes a node with reference hardware to execute it

Autonomys separates transaction fees paid by network participants into:

* **Storage fees**: For the storage space consumed by including a transaction in a block and archiving it
* **Compute fees**: For the computational resources consumed by the execution of the transaction

### Storage fees

The size of the storage fee depends on the length of the transaction and the amount of available storage on the network. The formula for the storage fee is:

$$storage\_fee\_per\_byte = total\_credit\_supply / total\_space\_pledged/min\_replication\_factor-history\_size * (shannons/byte)$$

$$storage\_fee(tx)=storage\_fee\_per\_byte∗length(tx)\ shannons$$

For the purposes of storage fee calculation, the total $AI3 supply consists of all $AI3 in existence, including staked or otherwise locked $AI3. The total space pledged to the network is divided by the protocol's minimum replication factor of 50, ensuring that the network is able to reliably store all the transactions included in the consensus chain. The history size is the total size of all the blocks in the consensus chain that are archived.

### Compute/execution fees

The size of the compute fee depends on the weight of the transaction and the demand on the network. Compute fees for the execution of extrinsics on the consensus chain (e.g. balance transfers) are collected by the block proposer. Compute fees for executing transaction bundles on domains are split equally between the domain operators who submitted the execution receipt (ER) containing the bundle (after the ER has cleared the challenge period).

Autonomys implements Polkadot’s [slow adjusting fee](https://research.web3.foundation/Polkadot/overview/token-economics#2-slow-adjusting-mechanism) mechanism where the fee is slightly adjusted each block based on the utilization of the available block weight by normal extrinsics.

The formula for the compute fee is:

$$compute\ fee(tx) = adjustment\ multiplier * compute\ fee\ per\ weight * weight(tx)\ shannons$$

## Dynamic issuance

The issuance of the newly minted tokens by the protocol is dynamic, depending on recent demand for blockspace and a decay function that gradually reduces rewards over 40 years. This smooth reduction allows for higher rewards for early adopters, a gradual increase in the circulating supply in a more controlled manner, and an extended lifetime of issuance for the long-term viability of the chain.

For more information on Autonomys' sustainable token issuance model, read our [token paper](https://www.autonomys.xyz/post/from-space-race-to-long-tail-crafting-a-sustainable-token-issuance-model-for-a-resilient-autonomys-network).

For full details of $AI3 supply and distribution, read the [Subspace Foundation paper](https://www.subspace.foundation/autonomys-network-token-supply-and-distribution).
