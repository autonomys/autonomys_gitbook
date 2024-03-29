# Our response - Auto Score

As we pointed out [before](introduction-to-proof-of-personhood.md), current solutions to proof-of-personhood suffer from a trade-off between security and user-friendliness. Most solutions have a clear disadvantage: social voting is not scalable. Worldcoin’s orbs, which analyze biometric data, could present a backdoor that would hamper them from supporting the revocation of identity when a problem gets identified. To be scalable, efficient and secure, the system should have no biometrics collection, should be open-source from top to bottom and should have a mechanism for claiming and re-issuing the identity.

Auto ID aims to provide an Auto Score, a probability rating that a given entity is a human. We will leverage the foundations laid by existing proof-of-personhood protocols, as well as other services that support identity claims, such as OIDC providers and government registries. Claims linking an Auto ID to a wide range of services will allow users to construct a profile that offers different levels of "proof" of their personhood.

This information can then be aggregated into their Auto Score that can be presented to a service that requires some minimum probability of human-ness in order to interact with it. Creating an Auto Score from a user's identity claims can be approached in various ways, each tailored to specific use cases. Currently, we are actively researching and refining the scoring methodology.

<figure><img src="../../../../.gitbook/assets/Screenshot 2024-03-11 at 2.36.17 PM (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/Screenshot 2024-03-11 at 2.36.24 PM.png" alt=""><figcaption></figcaption></figure>

**Essence of the Solution**: We propose a service that supports varying levels of proof with corresponding levels of user-friendliness. We will create an interface for proof-of-personhood—a registry that aggregates all evidence of personhood. It may contain very little evidence or an abundance of evidence. It is completely optional to the user. The amount and quality of evidence will contribute to a user’s “auto score”—a score that indicates the likelihood of a particular user being human.



