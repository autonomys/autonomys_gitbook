---
description: Ensuring secure communication between chains on the Autonomys Network
---

# Cross-Domain Messaging (XDM)

**Cross-domain messaging (XDM)**, is a core innovation within the Autonomys Network designed to enable seamless, secure, and trustless communication between the **consensus chain** and various specialized execution environments, known as **Domains**.

### Why Cross-Domain Messaging?

Decentralization is most powerful when paired with flexibility and interoperability. In a modular blockchain architecture, different components—such as consensus, execution, and storage—are separated to enhance scalability, specialization, and innovation. But how do these distinct blockchain components communicate effectively?

That's precisely where XDM comes into play.

By creating standardized pathways for data, asset transfers, and messages to move between separate domains, the Autonomys Network achieves true interoperability without compromising security or decentralization. Whether you’re moving tokens, sharing application state, or executing cross-chain actions, XDM provides the robust infrastructure to make it happen seamlessly.

### Core Components of XDM

To fully understand cross-domain messaging, let’s introduce two important concepts at its core: **Channels** and **Messages**. Together, these form the backbone of secure, efficient, and reliable cross-domain interactions.

#### Channels: Trusted Communication Pathways

In XDM, a **Channel** acts like a secure, dedicated connection between two distinct domains or between a domain and the consensus chain. Think of channels as specialized tunnels that safely guide messages from their source to their destination, ensuring nothing is lost or altered along the way.

Each channel is uniquely identified by the specific domains it connects, providing clarity and precise routing for every message it carries. Before communication can begin between domains, a channel must first be opened. Once established, this channel is responsible for keeping track of message order, security checks, and reliability throughout its lifetime.

#### Messages: Packets of Information

If channels are secure pathways, then **Messages** are the packets of information traveling along these paths. Messages in XDM can represent asset transfers, state updates, or simple communications between applications running on separate domains.

Each message includes clear information about:

* **Sender**: The origin domain and application initiating the communication.
* **Recipient**: The intended destination domain and application.
* **Payload**: The actual data or instructions being transmitted, such as token transfers or state changes.

By carrying structured information, messages ensure clarity and accountability at every step.

#### Lifecycle: How Channels and Messages Work Together

Here's how channels and messages collaborate throughout their lifecycle to deliver reliable cross-domain communication:

**1. Channel Initialization**

First, domains or applications that need to communicate initiate a new channel. This involves a handshake process where both sides recognize and trust the pathway for future messaging.

**2. Message Submission**

Once a channel is active, an application submits a message to its domain's runtime. The domain securely records this message in its internal state, preparing it for inclusion in the next block.

**3. Message Commitment & Relaying**

The domain's runtime includes the committed message in a new block, which is then relayed securely to the consensus chain.

**4. Verification on the Consensus Chain**

Upon receiving the block, the consensus chain verifies the message's authenticity and confirms it matches the established channel and sender details.

**5. Challenge Period**

A brief security window called a challenge period follows. During this time, validators and participants can ensure no discrepancies or malicious activities occurred. This provides robust security guarantees.

**6. Dispatching & Delivery**

After successfully passing the challenge period, the consensus chain safely dispatches the message to its intended recipient domain via the previously established channel.

**7. Acknowledgment and Response**

Upon receiving the message, the recipient domain processes it accordingly, potentially sending back an acknowledgment or follow-up message through the same secure channel.

#### Channel Management and Security

Secure communication between domains also depends on robust channel management:

* **Channel Closure:** Channels can be closed by either domain through a secure, protocol-driven message. Closure ends communication immediately, preventing further exchanges.
* **Channel Deposits:** A financial deposit is required to establish a channel, deterring misuse and denial-of-service (DoS) attacks by making malicious activities economically infeasible.

#### Why It Matters

By clearly defining channels and messages and meticulously managing their lifecycle, Autonomys’ XDM ensures seamless, trustless, and verifiable communication across decentralized domains. This structure safeguards the integrity of data, assets, and interactions, making cross-domain cooperation intuitive and secure for everyone involved.

### Fee Model

Cross-domain messaging incorporates a transparent and fair fee structure to incentivize domain operators and ensure system sustainability:

* **Compute Fees:**
  * Computed based on the processing requirements of each message on both sender and receiver domains.
  * Initially collected from the sender and burned on the originating domain. After successful delivery and execution, fees are minted on the receiving domain and distributed to operators.
* **Relay Fees:**
  * Compensate the operators relaying messages between domains.
  * Collected from the sender, burned on the sending domain, and minted on the receiving domain upon successful delivery.

### XDM in Action: Connecting Autonomys Together

The powerful combination of a trusted consensus intermediary, distinct specialized domains, unique identification, and a meticulously designed message lifecycle makes XDM one of Autonomys Network’s defining innovations.

Through XDM, decentralized applications built on different domains within Autonomys can interact effortlessly - creating a cohesive ecosystem greater than the sum of its parts. Assets and data can move fluidly, applications can collaborate across domains, and users benefit from enhanced functionality and reliability.

XDM is the connective tissue holding Autonomys Network together, ensuring seamless interoperability while preserving decentralization and security at every step.

Further reading can be found in the [protocol specs](https://github.com/subspace/protocol-specs/blob/main/docs/decex/xdm.md).
