---
description: >-
  An overview of Autonomys' novel mechanism for communication between domains
  and the consensus chain
---

# Cross-Domain Messaging (XDM)

**Cross-domain messaging (XDM)** enables seamless, secure and trustless communication between [domain](../) chains and the Autonomys Network [consensus](../../consensus/) chain at the protocol level by creating standardized, verifiable cross-chain pathways for sharing data, assets, and messages.

XDM allows Autonomys' modular architecture of specialized components to interoperate efficiently, while preserving their separation for optimized scalability, security and decentralization. This facilitates the development of scalable dApps built across multiple domains, and the creation of a cohesive and intuitive Autonomys ecosystem.

Further technical information is available in our [protocol specs](https://github.com/subspace/protocol-specs/blob/main/docs/decex/xdm.md).

## Components

### Channels

Channels are secure, dedicated communication pathways between domains or between a domain and the consensus chain. Each endpoint pairing has a uniquely identifiable specialized channel, ensuring clear and precise message routing. Once a channel is opened, it is responsible for maintaining message order, security checks, and reliability throughout its lifetime.

#### Channel Management and Security

* **Channel Opening:** A financial deposit is required to establish a channel, deterring misuse and denial-of-service (DoS) attacks by making malicious activities economically infeasible.
* **Channel Closure:** Channels can be closed by either domain through a secure, protocol-driven message. Closure ends communication immediately, preventing further exchanges.

### Messages

Messages are packets of information that travel along channels. They may represent asset transfers, state changes, or simple communications between dApps running on separate domains.

Each message includes clear information about the:

* **Sender**: The origin domain and application initiating the communication
* **Recipient**: The destination domain and application receiving the communication
* **Payload**: The data or instructions being transmitted

By carrying structured information, messages ensure clarity and accountability at every step.

## Workflow

1. **Channel Initialization:** A domain or application requiring cross-chain communication initiates a new channel via a handshake process where both sides recognize and trust the channel for future messaging.
2. **Message Submission:** Once a channel is opened, applications can submit messages to the domain's runtime. The domain securely records these messages in its internal state, preparing them for inclusion in the next block.
3. **Message Commitment & Relaying:** The domain's runtime includes the committed messages in a new block, which is then relayed securely to the consensus chain.
4. **Consensus Chain Verification:** Upon receiving the block, the consensus chain verifies the messages' authenticity, and confirms the channel, sender and recipient details are accurate.
5. **Challenge Period:** The challenge period is a brief security window during which validators and participants ensure no discrepancies or malicious activities have occurred, providing robust security guarantees.
6. **Dispatchment & Delivery:** After successfully passing the challenge period, the consensus chain securely dispatches the messages to their intended recipient domain via the previously established channel.
7. **Acknowledgment and Response:** Upon receiving a message, the recipient domain processes it accordingly, optionally sending back an acknowledgment or follow-up message through the same secure channel.
