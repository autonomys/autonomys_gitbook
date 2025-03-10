---
description: An overview of staking on the Autonomys Network
---

# Staking

The Autonomys Network relies on staking from both domain [operators](../network-architecture.md) and nominators (who are mostly farmers) to secure the network. Under Autonomys' Nominated Proof-of-Stake (NPoS) algorithm, nominators endorse operators who execute transactions and produce blocks, with operator stakes acting as nomination pools. NPoS allows all $AI3 token holders with the required minimum stake (MinStake) to participate in staking and earn a yield on their holdings, maintaining high levels of network security by increasing total value locked (TVL). A significant portion of the total $AI3 supply is likely to be staked in the NPoS system at any one time.

Autonomys uses a two-tier staking model:

* **Operators** stake an $AI3 MinStake to join a [domain](domains/) (set by the domain creator), earning the right to produce blocks and [$AI3 rewards](../rewards-and-fees/) (execution fees) in exchange for validating and executing transactions, producing execution receipts, and applying state transitions. Operators set a nominator MinStake and nomination tax for their pool when they register. The nomination tax is the operator's share of the execution fees, and is automatically re-staked. Operator slot leader elections to determine block production are stake-weighted for each domain.
* **Nominators** stake an $AI3 MinStake to operators (increasing their stake and chance of success in slot leader elections) and earn a share of their fees. An unlimited number of nominators can stake to an operator's nomination pool. Nominators are often farmers earning $AI3 rewards for pledging storage, but any $AI3 token holder can nominate.

This system balances power between nominators/farmers and operators, with both parties sharing the operator fees and potential penalties (via slashing). As nominators can easily stake and un-stake at any time, operators are incentivized to recruit and compete for nominators by cultivating a trusted community reputation, providing good service, and offering a reasonable nomination tax, ensuring they remain accountable.

Autonomys' two-tier staking structure also provides robust security guarantees by consolidating quantities of stake far exceeding the size of any one $AI3 holding, creating significant barriers for bad actors attempting to elect dishonest operators. Attacking the system would be both prohibitively expensive (as large amounts of stake would be slashed) and require considerable community trust (to attain the necessary stake), making it highly challenging for adversaries.

## Staking epochs

A staking epoch is a period of time during which staking distribution remains the same. This period is currently set to 100 blocks (\~10 minutes). The end of each epoch triggers a series of events to transition to the next epoch. These events include:

* allocation of fees earned for the blocks confirmed during the epoch
* deposits and withdrawals of stake
* operator registrations and de-registrations
* recalculation of stake distribution for the slot leader election

New operators must therefore wait for the end of the current epoch to register; new nominators must wait to nominate; and new stake deposits and withdrawals must wait to be processed. As soon as the end of the epoch transition is finalized, the next epoch begins.

<picture><source srcset="../../.gitbook/assets/Nomination-dark.svg" media="(prefers-color-scheme: dark)"><img src="https://subnomicon.subspace.network/img/Nomination-light.svg#gh-light-mode-only" alt="Nomination"></picture>

## Nomination pools[​](https://subnomicon.subspace.network/docs/decex/staking#nomination-pools) <a href="#nomination-pools" id="nomination-pools"></a>

Any $AI3 token holder with the required nominator MinStake can join an operator's nomination pool by submitting a nomination transaction with their desired $AI3 stake deposit. The workflow is then as follows:

1. The nominator's $AI3 deposit is added to the list of pending deposits in the nomination pool.
2. At the end of the epoch, the nominator's deposit is processed.
3. 20% of each nominator's deposit is reserved in the operator's storage fee fund to pay for bundles the operator creates. This does not affect the stake distribution and is proportionally refunded with each withdrawal. The remaining 80% is locked in the nominator's wallet.
4. The nominator's share of the total pool is calculated based on their deposit as a percentage of the total stake and their length of time staked. This is used to calculate the nominator's share of the operator's execution fees as follows:
   1. Compute the nomination pool end-of-epoch $$shares\_per\_AI3$$ as the total number of shares divided by the sum of all stake in the pool and fees collected during the previous epoch:\
      $$shares\_per\_AI3 = total\_shares/(pool\_total\_stake + fees∗(1−nomination\_tax))$$
   2. Assign the $$shares$$ to the nominator based on the $$shares\_per\_AI3$$ of the pool:\
      $$shares = deposit\_amount * shares\_per\_AI3$$
   3. Add the $$deposit\_amount$$ to the $$pool\_total\_stake$$ of the nomination pool and the domain’s total stake
   4. Add the $$shares$$ of the nominator to the $$total\_shares$$ of the nomination pool

Autonomys nomination pools are 'lazy'—any execution fees earned by operators are automatically re-staked to the pool, and not deposited to nominator wallets until a withdrawal request is submitted. This increases the pool's total stake and the operator's chance of producing blocks. Nominator withdrawal requests are processed at the end of the epoch, at which point the nominator's stake is removed from the pool and the domain's total stake, and they receive their share of the fees.

Operators can also withdraw their stake and fees at any time by submitting a `withdraw_stake` extrinsic. To withdraw their entire stake and earned fees, an operator must deregister (as they would no longer satisfy the domain's MinStake requirements). Deregistered operators are removed from the domain, and their stake, as well as the stakes of all their nominators, are returned to their wallets.

Withdrawals currently have a locking period of 14,400 domain blocks (\~1 day), after which withdrawn tokens are unlocked in users' wallets. All withdrawals requested in the same stake epoch are aggregated together, and the total amount is unlocked at once. This locking period is necessary to ensure that the domain block executing the withdrawal is confirmed and not challenged by a fraud proof, increasing the economic stability of domains.

<picture><source srcset="../../.gitbook/assets/Nomination_Pool-dark.svg" media="(prefers-color-scheme: dark)"><img src="https://subnomicon.subspace.network/img/Nomination_Pool-light.svg#gh-light-mode-only" alt="Nomination pool"></picture>

## Example[​](https://subnomicon.subspace.network/docs/decex/staking#example) <a href="#example" id="example"></a>

Operator $$O$$ has registered an operator with a nominator MinStake of 10 $AI3 and nomination tax of 5%, and staked 100 $AI3. Operator $$O$$ has 2 nominators $$N_1$$ and $$N_2$$​, each staking 50 $AI3. Initially, $$shares\_per\_AI3 = 1$$, so $$O$$ receives 80 shares, $$N_1$$​ and $$N_2$$ each receive 40 shares, and $$total\_shares = 80 + 40 + 40 = 160$$ in the stake. 20% of each deposit is reserved in a storage fee fund: $$O$$ reserves 20 $AI3, and $$N_1$$​ and $$N_2$$​ reserve 10 $AI3 each, for a total fund of 40 $AI3:

|                         | $$O$$   | ​$$N_1$$​ | $$N_2$$​ |
| ----------------------- | ------- | --------- | -------- |
| **Shares**              | 80      | 40        | 40       |
| **Storage fee deposit** | 20 $AI3 | 10 $AI3   | 10 $AI3  |

<table><thead><tr><th>Total stake</th><th>Total shares</th><th width="196">Total storage fee deposits</th><th>Storage fee fund</th></tr></thead><tbody><tr><td>160 $AI3</td><td>160</td><td>40 $AI3</td><td>40 $AI3</td></tr></tbody></table>

In the next epoch, the pool earns 20 $AI3 in execution fees and is refunded an extra 4 $AI3 in storage fees. The operator takes a 5% nomination tax (1 $AI3) on the execution fees, which is automatically re-staked for 1 share, and of which 0.05 $AI3 is deposited to the storage fee fund. The pool stake is now $$160 + 20 + 1 = 181$$ $AI3; the storage reserve is now $$40+4=44$$ $AI3; and the pool end-of-epoch $$shares\_per\_AI3$$ is now $$160/(160+20*(1−0.05))=0.893855$$. The refunded 4 $AI3 in storage fees is not calculated as part of $$shares\_per\_AI3$$, maintaining a stable stake distribution despite the fluctuating size of the storage fee fund.

A new nominator $$N_3$$​ stakes 33.6 $AI3. 6.72 $AI3 is transferred to the storage fee fund, and $$N_3$$​ receives $$((33.6−6.72)*0.893855)=24$$ shares. The total pool stake becomes $$181+26.88=207.88$$ $AI3; the storage fee reserve becomes 50.72 $AI3; and the total shares becomes $$160+24+1=185$$.

The updated staking summary at the end of the epoch:

|                         | $$O$$      | $$N_1$$​ | $$N_2$$​ | $$N_3$$​​ |
| ----------------------- | ---------- | -------- | -------- | --------- |
| **Shares**              | 81         | 40       | 40       | 24        |
| **Storage fee deposit** | 20.05 $AI3 | 10 $AI3  | 10 $AI3  | 6.72 $AI3 |

<table><thead><tr><th>Total stake</th><th>Total shares</th><th width="198">Total storage fee deposits</th><th>Storage fee fund</th></tr></thead><tbody><tr><td>207.88 $AI3</td><td>185</td><td>46.72 $AI3</td><td>50.72 $AI3</td></tr></tbody></table>

Suppose that after some time, $$N_1$$ wants to withdraw 20 shares; $$shares\_per\_AI3$$ in the pool is 0.8; and the storage fee fund balance is 52 $AI3. At the end of the epoch, the 20 shares are un-staked, and the corresponding amount of $AI3 ($$20/0.8=25 AI3$$) is deducted from the pool's total stake. The total amount of $AI3 $$N_1$$ receives is:

$$(withdraw\_shares/shares\_per\_AI3) + storage\_fee\_fund\_balance * (storage\_fee\_deposit/total\_storage\_fee\_deposits) * (withdraw\_shares/shares) = 25 + 52 * (10/46.72) * 20/40 = 30.57 AI3$$

If $$N_1$$ wanted to withdraw all their stake and fees (40 shares), they would receive: $$(40/0.8) + 52 * 10/46.72 * 40/40 = 61.13 AI3$$, earning 11.13 $AI3 in fees. After waiting the locking period, the withdrawn amount is unlocked in their wallet.

> _Note:_ This example is intended for illustration. The actual calculations are performed with shannons $$(1 AI3 = 10^{18}$$ shannons).
