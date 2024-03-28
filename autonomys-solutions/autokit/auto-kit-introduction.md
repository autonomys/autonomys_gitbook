# Auto Kit Introduction

At this point, we’ve discussed in great detail what AutoID is and how blockchain finally finds the real use case scenario and becomes a guardrail for AI to make sure humanity and AI can safely coexist together and collaborate effectively at scale. The question is - what would drive the adoption? How do we ensure that the idea behind AutoID is heard and understood? How do we onboard millions and billions of users? The answer to all those questions is Auto Kit.

#### What is the Auto Kit?

Auto Kit is a Software Development Kit (SDK) that allows AI and Web developers to easily interact with the Autonomys Network through familiar programming languages like Python and Javascript, without needing to understand how blockchains or smart contracts work. It exposes simple APIs for issuing and verifying Auto IDs, as well as sending and accepting payments using Auto Cash. The key point in the section above is simplicity - every user interaction with Auto ID needs to be seamless, and there should be no barriers or ambiguity in any action the user takes, it just has to work out of the box. It’s powerful and essential, but simple and transparent at the same time.

#### What programming language Auto Kit is written with?

The initial implementation is written with Python - one of the most easily readable programming languages in the world. It’s fully open source and can be viewed here (to do: link to the Github). The implementation of AutoID is also open source (to do: link to Github) and written in one of the most secure programming languages - Rust.

#### What programming language I can interact with Auto Kit?

We primarily focusing on AI developers who use Python and Web-Developers who use JavaScript. As the Auto ecosystem evolves to encompass AutoFi and AutoCo, the SDK will expand its capabilities to support development on top of these additional platforms, enabling developers to build a wide range of applications and services within the Auto ecosystem. This is an exciting journey and we’re more than happy to consider any community contributions.

#### Core components of Auto Kit

1. **Auto ID** provides _**identification**_ for autonomous entities using a simple, extensible, and X.509 compatible standard for binding self-selected public identifiers to self-generated public keys through digital signatures, across an array of conceivable issuance and registration models.
2. **Auto AuthN** provides _**authentication**_ for autonomous entities by using Auto ID certificates over any Transport Layer Security (TLS) channel, where each entity validates certificates based on their chosen trust model and its associated Public Key Infrastructure (PKI).
3. **Auto AuthZ** provides _**authorization**_ for autonomous entities through compatibility with the Open Authorization (OAuth) and Open ID Connect (OIDC) protocols, allowing identity and access claims to be delegated and bound to an Auto ID by using nested digital signatures.

#### We will dive deeper into the nuts and bolts of what the SDK is, interacting with the SDK, and will discuss the potential applications in the next sections.
