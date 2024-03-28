# How can developers use Auto ID

#### How Can Developers use Auto ID?

**Auto SDK:** Developers can create applications and services for entities that hold Auto IDs using the Auto SDK. This SDK provides developers with three things: a simple account model for issuing digital identities to autonomous entites; an authentication system that allows entities to prove they hold a given identity, and an authorization framework for delegating identity and access claims between entities.

1. **Auto ID** provides _**identification**_ for autonomous entities using a simple, extensible, and X.509 compatible standard for binding self-selected public identifiers to self-generated public keys through digital signatures, across an array of conceivable issuance and registration models.
2. **Auto AuthN** provides _**authentication**_ for autonomous entities by using Auto ID certificates over any Transport Layer Security (TLS) channel, where each entity validates certificates based on their chosen trust model and its associated Public Key Infrastructure (PKI).
3. **Auto Authz** provides _**authorization**_ for autonomous entities through compataibility with the Open Authorization (OAuth) and Open ID Connect (OIDC) protocols, allowing identity and access claims to be delegated and bound to an Auto ID by using nested digital signatures.

In summary, Auto provides developers with a common standard for identifying, authenticating, and authorizing autonomous AI entities, in a way that is backwards compatible with widely-adopted standards such as X.509 PKI certificates, communication over TLS, as well as the OAuth and OIDC protocols. Moreover, any two autonomous entities with an Auto ID may securely communicate, regardless of implementation, provider, or platform.
