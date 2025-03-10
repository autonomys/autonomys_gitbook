---
description: A comparison of different ecosystem rollup architectures
---

# Taxonomy

## Standard rollups

Standard rollups (on Ethereum) are validated and settled through smart contracts.

## Sovereign rollups

Sovereign rollups (on Celestia) leverage the base layer protocol for consensus and data availability.

## Enshrined rollups

Enshrined rollups (domains on Autonomys) are directly integrated into the core consensus protocol of the underlying blockchain, ensuring the rollup's features and functionality are maintained and enforced by the network's consensus rules. This built-in support enhances the rollup's security, interoperability and adoption, while providing the benefits of a typical rollup, such as increased throughput and reduced transaction fees.

Domains extend Celestia's sovereign rollup model to include shared settlement by default by allowing operators to re-stake (as proposed by Free2Shard and implemented by EigenLayer on Ethereum). Autonomys enshrines the re-staking model within the semantics of the core protocol (unlike EigenLayer, which is implemented through smart contracts).

Although similar to Polkadot parachains, domains support a modular validation framework and permissionless deployment, unlike parachains' monolithic validation model and permissioned deployment. Domains also have shared security and trust-minimized interoperability as they are validated and settled on the consensus chain (unlike Cosmos zones and Avalanche subnets).
