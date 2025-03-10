---
description: An overview of Autonomys domain sub-protocols
---

# Domains

## Workflow

### Domain creation

To create a domain, a developer registers and uploads the domain runtime to the chain state, before instantiating the domain on the registered domain runtime. The domain instantiation process includes a genesis config for specifying variables including the domain name, runtime code, maximum block size and weight, and number of bundles in each slot and block (from which the chainspec and genesis block for the domain are built).

### Operator staking

Operators can begin participating in leader elections to produce domain bundles and execute blocks by submitting a registration extrinsic with a staking deposit to a domain. This will add them to the domain's Operator Registry and allow them to participate in the leader election at the next stake epoch. Nominators can then begin staking $AI3 to those operators.

### Domain transactions

Users can start producing extrinsics (transactions) and submitting them to domains once an operator has joined the domain. When pre-validating extrinsics, operators only check to ensure the extrinsic is well-formed and that the user can afford the blockspace storage fee. They do not yet attempt to execute the transaction (which will determine whether the execution weight fees can be paid).

### Leader election

For each time slot, all registered operators attempt to solve a VRF puzzle for leader election (with a success probability defined in the domain genesis config) by signing the slot challenge and checking if the result is below the desired threshold. The elected operator gathers transactions from the pool and produces a new domain bundle.

### Bundle production

To produce a new bundle, an operator must include:

* a proof of election showing that they are a leader for this time slot
* an execution receipt that either extends or confirms the previous domain block tracked on the consensus chain
* all bundle extrinsics that fall within the operator's portion of the extrinsic pool
* storage fees for the bundle extrinsics

If all is provided, the bundle is broadcast on the consensus chain gossip network.

### Bundle verification

All consensus (farmer) nodes receiving the bundle verify that it is well-formed. The bundle header should include a valid proof of election based on the stake distribution for the relevant epoch, and the execution receipt should build on the current execution chain block tree for this domain. Consensus nodes broadcast all valid bundles to their peers and place them within their local extrinsic pool.

### Bundle inclusion in the consensus block

Once a consensus node is elected to produce a new consensus chain block, it includes as many valid domain bundles as will fit into the block, before broadcasting the block to the consensus network. Other nodes will only accept blocks that include valid bundles.

### Domain block execution

Operators can build and execute domain blocks with the corresponding valid consensus block (if it contains at least one domain bundle). On block execution, each bundle header is applied to the consensus chain state, and each extrinsic is added to the domain's execution inbox. Extrinsics are deduplicated, grouped by sender, and deterministically shuffled to mitigate the ability of operators to extract value from users by re-ordering or inserting extrinsics (MEV). The domain block is then carefully executed, one extrinsic at a time, allowing the operator to produce an execution receipt.

### Challenging operators

Any node that observes an execution receipt within a bundle of any consensus chain block that differs from what they produced locally, produces an extrinsic with a fraud proof to handle this detected fraud. If the fraud proof is valid, it will be included in the consensus chain, which will prune the execution receipt in question and all children from the block tree, and slash all related operators. Currently, the challenge period is 14400 domain blocks (\~1 day).

### Domain block fees

A domain block is considered confirmed and can no longer be disputed when its challenge period ends.    Domain block fees are made up of execution and storage fees as well as tips included with the block's transactions. After a domain block is confirmed, the total fees for the block are applied as follows:

* The storage fees of the confirmed block are refunded to the operators that authored bundles in the block according to the respective storage sizes of their bundles.
* The execution fees of the confirmed block are added to the current epoch fees for the relevant domain, and split equally between the pools of operators that submitted the execution receipt for the block. The current epoch fees are noted in the Operator Registry until the epoch transition. All fees are auto-staked to the pools' stakes at the end of the current epoch (see [Staking](../staking.md#staking-epochs) for more details on staking epochs).
* Operators receive a share of all fees earned by their pool (as per the nomination tax specified in their operator config). This is automatically re-staked to each operator at the next epoch transition, and operator shares, total pool shares, and total stake are updated (see [Staking](../staking.md#example) for an example share calculation).
* The domain applies all changes related to fees and (un)staking to operators at the next epoch transition (note that this only changes the total pool balance and does not affect individual nominator shares).

<figure><img src="../../../.gitbook/assets/infographic-domain-transaction-flow (1).png" alt=""><figcaption><p>Domain transaction flow from submission to fee distribution</p></figcaption></figure>

## Permissionlessness

* **Creating** **a domain** is _permissionless._
* **Staking** and **nomination** are _permissionless_, meaning operators and nominators can freely stake and unstake across different domains.
* **Operating** on most domains is _permissionless_ provided the prospective operator has the required funds for the minimum stake (MinStake). Some domains may choose to restrict who can operate on them via an allowlist, but this is not the default.
* **Opening a cross-domain messaging channel** must be allowed by both domain owners.
* **Registering a new runtime** to create a non-WASM, EVM or Substrate-based domain is permissioned, requiring protocol governance approval.
