# Autonomous Identity (Auto ID)

## Autonomous Identity

Auto ID is a digital identity framework for the AI age. It gives everyone the ability to distinguish between humans and AI online by providing developers with the tools they need to easily identify, authenticate, and authorize AI systems. Auto is built on the following core beliefs.

1. To maintain online trust in the age of AI, we need a method for distinguishing between different kinds of _**autonomous**_ entities online. These include: natural entities, such as human beings and organizations; artificial entities, such as AI systems; or some combination thereof.
2. To maximize _**autonomy**_, or freedom, for all entities across the Internet, an ideal digital identity framework should only provide a few key building blocks, allowing developers to express a variety of digital trust models, which entities may opt-into based on their preferences.
3. To manage the ever-increasing complexity required to maintain online trust, we must leverage _**automation**_ to the greatest extent possible. This includes supporting password-free authentication, smart credential management platforms, and AI assitance where appropriate.

#### Auto ID

Autonomous Identity (Auto ID) is our solution to this problem. Auto ID is a new form of digital identity, rooted in public key cryptography, that may be issued to both humans and AI. Auto ID is based on the Auto PKI, a decentralized form of Public Key Infrastructure (PKI) that anyone or anything may use to register and verify online identity.

Auto ID builds trust by allowing everyone to identify both AI and humans online, authenticate the content they produce, and authorize AI to act on their behalf. Unlike World ID, which may only be issued to humans through the Orb, a biometric scanning device, Auto ID may be issued to any autonomous entity via an online portal or API. Entities may then attach any cryptographic identity claim, such as a World ID, to their Auto ID, allowing them to _compose_ a proof-of-personhood.

#### What is an Auto ID?

An Autonomous Identity (Auto ID) is new form of universal digital identity that is defined by a handful of basic rules.

1. Anyone or anything that can be considered an _entity_ may have an Auto ID
2. Any natural entity, such as human being or institution, may self-issue its own Auto ID
3. Any artificial entitiy, such as an AI system, must be issued its Auto ID by a natural entity
4. Two or more entities working together may jointly issue a composite Auto ID
5. Every Auto ID must have a unique public identifier, similar to a username
6. Every Auto ID must have a cryptographic key pair, similar to a password
7. Every Auto ID must be certified by the issuer’s private key, which may be its own
8. An Auto ID may include any number of internal claims, which its issuer must attest to
9. An Auto ID may be linked to any number of external claims, which anyone may attest to
10. An Auto ID should be registered within a public database, allowing for open verification

#### What are the benefits of Auto ID?

From these rules, we may derive several key properties of an Auto ID that benefit everyone

* _Verifiable_: Through the use of digital signatures, control over an Auto ID, and the legitimacy of any granted claims may be authenticated by anyone with the related public keys.
* _Portable_: An Auto ID is a self-contained digital document that is not inherently tied to any paritcular online provider or public registry, allowing it to easily move across platforms.
* _Backwards Compatible_: Auto IDs simple structure is compatible with X.509 Public Key Infrastructure (PKI) certificates and the Open ID Connect (OIDC) account model.
* _Secure_: Using mutual Transport Layer Security (mTLS) , any two entities with an Auto ID may establish an authenticated and encrypted communication channel over a public network.
* _Interoperable_: Since an Auto ID is based on a common standard, any entity with an Auto ID may grant claims against any other entity
* _Linkable_: An Auto ID may act as a container for any number of identity claims or credentials, allowing to act as a universal digital passport for any type of digital identity.
* _Accountable_: Since every interaction between entites relies on digital signatures, which are non-repudiatable, all enties may be held accountable for their actions.
* _Revocable_: If an issuer chooses to register an Auto ID in a public database, then it may be revoked at any time, in a manner that is verifiable by anyone.
* _Recoverable_: if the entity holding an Auto ID loses access to its private key, then it may be issued a new one, either by the issuing entity, or if registered, by the database.
* _Traceable:_ If an Auto ID is registred in a public database, then provenance for its ownership and existence may be clearly established and verified by anyone.

#### Who may hold an Auto ID?

Since Auto ID is designed to maximize flexibility and accessability, it may be issued to any type of abstract or concrete _entity_ which has a digital footprint. Some examples include:

* Any human being may hold its own Auto ID
* Any human organization or instuition may hold its own Auto ID
* Any online service or platform may hold its own Auto ID
* Any user of an online platform may be issued an Auto ID
* Any software application may be issued an Auto ID by its creator
* Any online platform may issue an API key to any developer as an Auto ID
* Any AI model may be issued an Auto ID by its creator
* Any instance of an AI model exposed to a user, may be issued an Auto ID
* Any autonomous AI software agent may be issued an Auto ID
