# Using Auto ID

#### How Can Someone Create and Register an Auto ID?

**Auto App:** Anyone can easily create an Auto ID using the cross-platform Auto mobile app. This app simplifies and automates the process of creating your Auto ID and managing your keys, while making it easy to link your Auto ID to existing accounts and services. The Auto app is fully open-source and does not rely on any backend servers or platforms to store your personal information or secret credentials. Everything runs locally on your device, allowing you to maintain full control over your digital identity.

**Auto Registry:** While entities are not required to register their Auto ID, registration does afford several benefits, including public verifiability, the ability to revoke delegate Auto IDs, and the ability to recover lost or stolen Auto IDs more easily achieved for a frictionless user experience. A valid Auto ID may be registered in any compatible public database. The default global auto registry is powered by the Subspace Network, an energy-efficient, massively-scalable, permissionless public blockchain. Anyone who can demonstrate a valid proof-of-personhood (an Auto ID with a high human score) may upload their Auto ID to the registry for free. This can be done through the public [LetsID.ai](http://letsid.ai) portal, provided by the non-profit Autonomys Association.

#### How Can Developers use Auto ID?

**Auto SDK:** Developers can create applications and services for entities that hold Auto IDs using the Auto SDK. This SDK provides developers with three things: a simple account model for issuing digital identities to autonomous entities; an authentication system that allows entities to prove they hold a given identity, and an authorization framework for delegating identity and access claims between entities.

1. **Auto ID** provides _**identification**_ for autonomous entities using a simple, extensible, and X.509 compatible standard for binding self-selected public identifiers to self-generated public keys through digital signatures, across an array of conceivable issuance and registration models.
2. **Auto AuthN** provides _**authentication**_ for autonomous entities by using Auto ID certificates over any Transport Layer Security (TLS) channel, where each entity validates certificates based on their chosen trust model and its associated Public Key Infrastructure (PKI).
3. **Auto Authz** provides _**authorization**_ for autonomous entities through compatibility with the Open Authorization (OAuth) and Open ID Connect (OIDC) protocols, allowing identity and access claims to be delegated and bound to an Auto ID by using nested digital signatures.

In summary, Auto provides developers with a common standard for identifying, authenticating, and authorizing autonomous AI entities, in a way that is backwards compatible with widely-adopted standards such as X.509 PKI certificates, communication over TLS, as well as the OAuth and OIDC protocols. Moreover, any two autonomous entities with an Auto ID may securely communicate, regardless of implementation, provider, or platform.
