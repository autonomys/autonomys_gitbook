---
description: An overview of Autonomys' decentralized identity framework
---

# Autonomys Identity (Auto ID)

**Autonomys Identity (Auto ID)** is our universal, self-sovereign [digital identity](../../autonomys-vision/use-cases.md#c.-digital-identity) framework for [the Age of Autonomy](../../autonomys-vision/intro-to-ai3.md), and a key building block for future [AI agent-augmented DAO governance](../../autonomys-vision/use-cases.md#j.-open-collective-intelligence-and-the-global-dao-mesh). Auto IDs allow anyone to verify the identity of humans and agents and the [provenance of the content](../../autonomys-vision/use-cases.md#b.-content-provenance-and-data-sovereignty) they create, fostering online trust and transparency in an increasingly AI-integrated world.

Based on the [Auto PKI](auto-pki.md), a decentralized public key infrastructure, Auto IDs can be self-issued by any natural entity (humans and organizations) and externally issued to any digital entity ([agents](../auto-agents.md), models, software, etc.) by any natural entity. Multiple entities can also jointly issue composite Auto IDs. Digital entities can be delegated authority via Auto ID, authorizing them to act on the issuer's behalf.

Each Auto ID has a unique public identifier (similar to a username) and cryptographic key pair (similar to a password). Auto IDs are registered on the public Auto Registry [domain](../../autonomys-network/decoupled-execution/domains/) on the Autonomys Network and certified by the issuer's private key. Users able to demonstrate a valid [proof-of-personhood](../../autonomys-vision/use-cases.md#d.-proof-of-personhood) (an Auto ID with a high [Auto Score](auto-score.md)) can register their Auto ID for free.

## Key features

* **Verifiable**: Anyone can verify the ownership provenance of an Auto ID and the legitimacy of its granted claims through the use of digital signatures and the relevant public keys (if the Auto ID is registered in a public database).
* **Portable**: Auto IDs are self-contained, and thus not inherently tied to any one provider or registry, allowing for easy movement across platforms.
* **Interoperable**: Auto IDs are based on a common, open standard and are compatible with [X.509 Public Key Infrastructure (PKI)](../../additional-learning/identity-security/public-key-infrastructure.md) certificates and the [Open ID Connect (OIDC)](../../additional-learning/identity-security/oauth-and-oidc.md) account model.
* **Secure**: Any two entities with Auto IDs can establish an authenticated and encrypted communication channel over a public network using mutual Transport Layer Security ([mTLS](https://www.cloudflare.com/en-gb/learning/access-management/what-is-mutual-tls/)), regardless of implementation, provider, or platform.
* **Universal**: Auto IDs can be linked to any number of identity claims or verifiable credentials, enabling them to act as universal digital passports.
* **Accountable**: All entities with Auto IDs can be held accountable for their actions via non-repudiable digital signatures stored on Autonomys' [DSN](../../autonomys-network/distributed-storage-network.md).
* **Revocable**: Auto IDs can be revoked at any time in a manner that is verifiable by anyone (if the issuer has registered their Auto ID in a public database).
* **Recoverable**: Entities can be issued a new Auto ID by their issuer (if not self-issued) or by the database (if self-issued and registered) if they lose access to its private key.

## Developers

The Auto SDK contains a simple account model for issuing digital identities to autonomous entities; an authentication system that allows entities to prove they hold a given identity; and an authorization framework for delegating identity and access claims between entities:

* **Auto ID** provides _**identification**_ for autonomous entities using a simple, extensible, and [X.509](auto-score.md)-compatible standard for binding self-selected public identifiers to self-generated public keys through digital signatures, across an array of conceivable issuance and registration models.
* **Auto AuthN** provides _**authentication**_ for autonomous entities by using Auto ID certificates over any Transport Layer Security (TLS) channel, where each entity validates certificates based on their chosen trust model and its associated Public Key Infrastructure (PKI).
* **Auto AuthZ** provides _**authorization**_ for autonomous entities through compatibility with the Open Authorization (OAuth) and Open ID Connect (OIDC) protocols, allowing identity and access claims to be delegated and bound to an Auto ID by using nested digital signatures.

In summary, the Auto SDK provides developers with a common standard for identifying, authenticating, and authorizing natural and digital entities in a way that is backwards-compatible with widely adopted standards such as X.509 PKI certificates, communication over TLS, and the OAuth and OIDC protocols.

To start building Auto ID-powered dApps and agents with the [Auto SDK](../auto-sdk.md), visit the [Autonomys Developer Hub](https://develop.autonomys.xyz) and [Auto SDK GitHub repository](http://github.com/autonomys/auto-sdk).

## Example: Demonstrating Provenance for AI-Generated Content

Alice uses an instance of an open-source AI model to help write content and generate images for her social media posts. She wants to show that her content is AI-generated. By linking her Auto ID to her user-specific instance of the AI model, she can demonstrate that the content she published was produced with that specific AI model at a specific time by digitally signing each piece of content and including a short proof-of-provenance alongside her post, meaning anyone can verify it.
