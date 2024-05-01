# Technical Implementation of Auto ID

### Agent ID

We propose a hybrid solution to the agent trust problem, referred to as Agent ID, which combines elements of a standard PKI system, existing IAM frameworks, and leading SSI proposals. Agent ID gives AI developers and Agent Providers (APs) a simple, open standard for securely identifying, authenticating, and authorizing AI agents online. Agent ID provides the three following concrete benefits:

1. Simplicity: Agent ID drastically simplifies the problem of building trustworthy agents, saving developers the significant time required to design and build their own system from scratch.\
   Interoperability:&#x20;
2. Interoperability: Agent ID is backwards compatible with any standard X.509 PKI, including the Web PKI. It is also interoperable with existing OIDC and OAuth providers, allowing humans to easily attach verifiable identity claims to their agents and delegate fine-grained access to their apps and services. Any Agent with an Agent ID may open a secure, private communicaiton channel with any other Agent that has an Agent ID, regardless of which programming language, developer framework, AI model, or Agent Provider the agent is based on. Agent ID may also be easily extendable to support SSI frameworks such as DIDs and VCs.
3. Safety: Agent ID ensures the human user is always in control of the agent by ensuring the user must always explicitly grant priveleges to the agent, while also being able to easily revoke any granted priveleges, including the Agent ID itself. Agent ID also provides the foundation for an accountability layer for agents, by creating a cryptographic log of all actors in the agent’s software supply chain and all of the actions undertaken by the agent on behalf of it user.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### Software Stack

Agent ID is comprised of an open standard and an open-source software stack provided as a reference implementation.

* _Agent ID Standard:_ A draft Internet Engineering Task Force (IETF) standards document defining the technical specification for the Agent ID protocol. This serves as a single source of truth for developers and architects building Agent ID compatible software and protocols.
* _Agent SDK_: A Software Development Kit (SDK) that implements the Agent ID standard in a manner that abstracts away the underlying Agent ID protocol details, while keeping it safe and easy to user for developers building agents in both Python and Javascript.
* _Provider Service_: An automated services that allows APs, such as Open AI or Rabbit, to grant verifiable credentials to any agents they host. These credentials allow agents to prove where they are hosted to third parties, creating a basis for trustworty and accountable interactions.
* _Controller App_: A cross platform mobile app for ordinary humans users, referred to as _conrollers_, which provides a simple way to interface with any agent that has an Agent ID. The app allows users to securely connect with agents, manage the agent’s credentials and delegate access to user credentials, regardless of which platform the agent is hosted on.
* _Registrar Service_: An automated service for registering Agent IDs issued by controllers in a verifiable manner. The registry acts a global transparency log that serves as the root of trust for the underlying PKI. Similar to Let’s Encrypt for TLS certificates, the registrar service is fully automated and free to use, allowing anyone to easily register their Agent ID.
