---
description: The Autonomys Network's AI3.0 infrastructure stack
---

# Architecture

Autonomys is a modular, hyper-scalable, storage-based Layer-1 blockchain network that decouples consensus from execution, dividing the core [PoAS consensus](consensus/) chain—maintained by [farmers](../auto-suite/spaceacres-cli/farmers.md)—from a nearly unlimited number of secondary [decoupled execution (DecEx)](decoupled-execution/) chains ([domains](decoupled-execution/domains/))—maintained by [operators](../auto-suite/spaceacres-cli/operators.md). Our extensive [distributed storage network (DSN)](distributed-storage-network.md) is a byproduct of the SSD space provided by our farmers to secure the network. The Autonomys Network is an instance of the [Subspace Protocol](consensus/) based on Substrate and written in Rust.

Our permissionless peer-to-peer network allows anyone with an SSD to join, permitting wide participation and engendering strong decentralization, while PoAS consensus ensures efficient data availability and environmentally friendly maintenance of the blockchain's state and immutable history. The modularity provided by our DecEx domains and DSN architecture enables unparalleled scalability and adaptability for developers building on the application layer. Domains support any state transition framework and execution environment, fostering cross-chain interoperability. Key innovations including [Auto ID](../auto-suite/auto-id/) and Auto Score—built on domains—provide a secure, verifiable identity system for both humans and AI entities that helps address the fundamental challenge of establishing trust in an increasingly AI-integrated world, at the same time as allowing for content authentication, and delegation of permissioned authority.

Autonomys' AI3.0 infrastructure stack, composed of four layers, forms a comprehensive ecosystem that abstracts away the complexities of blockchain development while enabling unprecedented scalability, security and flexibility for developers building any conceivable on-chain AI application:

{% include "../.gitbook/includes/autonomys-ai3.0-stack.md" %}

## Autonomys Network Visualization

{% embed url="http://youtube.com/watch?v=9jTBihUeq70" %}

<figure><img src="../.gitbook/assets/Autonomys illustration 1.jpg" alt=""><figcaption><p>Autonomys Network visualization</p></figcaption></figure>
