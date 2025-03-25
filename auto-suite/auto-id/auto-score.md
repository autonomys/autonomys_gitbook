---
description: An overview of Autonomys' proof-of-personhood protocol
---

# Auto Score

## Background

Current solutions to proof-of-personhood (PoP) suffer from a trade-off between security and user-friendliness. To be scalable, efficient, and secure, a system should be open-source from top to bottom, have no biometrics collection, and have a mechanism for claiming and reissuing identities.

## Auto Score

**Auto Score** is the sybil-resistant on-chain [proof-of-personhood](../../autonomys-vision/use-cases.md#d.-proof-of-personhood) framework utilized by Auto ID. An Auto Score is a measure of the probability of an entity's humanity calculated as a weighted aggregate of an Auto ID's verifiable online identities and credentials.

Auto IDs can include internal claims (attested by the issuer) and be linked to external claims (attested by anyone), such as OIDC providers (like Google and Apple), government registries or other PoP protocols (including [World ID](https://whitepaper.world.org/#world-id), which leverages biometric scanning to register unique human identities via [the Orb](https://whitepaper.world.org/#the-orb)).

Verifiable claims linking an Auto ID to a wide range of services contributes to a high overall Auto Score, as well allowing users to construct a profile that offers different levels of "proof" of their personhood. Solutions requiring some probability of humanity can then set a minimum Auto Score to permit interaction. Applications can also require specific identity claims be linked to an Auto ID for use.

## Example: Proving your Humanity Online

Alice wants to create an account on a new platform which uses captchas to prevent bots. If the platform integrates Auto ID sign-in, Alice can sign up with a single click using her Auto ID, as she has linked several existing verifiable online identities, including accounts for Google, Apple and X, that can attest she has a verified email and phone number. If an Auto ID with a human-level Auto Score is required to create a new account, the cost of sybil attacks is significantly raised, as a bad actor would have to generate or purchase multiple verified accounts across several reputable providers (to obtain a human-level Auto Score), as opposed to simply solving a captcha, before being able to sign up.
