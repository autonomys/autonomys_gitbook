# Auto Score Framework

As we pointed out [here](../../../additional-learning/ai-basics/proof-of-personhood.md), current solutions to proof-of-personhood suffer from a trade-off between security and user-friendliness. To be scalable, efficient, and secure, the system should have no biometrics collection, should be open-source from top to bottom, and should have a mechanism for claiming and re-issuing the identity.

Auto ID aims to provide an Auto Score, a probability rating that a given entity is a human. We will leverage the foundations laid by existing proof-of-personhood protocols, as well as other services that support identity claims, such as OIDC providers and government registries. Claims linking an Auto ID to a wide range of services will allow users to construct a profile that offers different levels of "proof" of their personhood.

This information can then be aggregated into their Auto Score that can be presented to a service that requires some minimum probability of human-ness in order to interact with it. Creating an Auto Score from a user's identity claims can be approached in various ways, each tailored to specific use cases. Currently, we are actively researching and refining the scoring methodology.\


### **The Auto Score Framework** [_This is an early outline of the Auto Score Framework. The steps and providers references below might and likely be changed or adjustment during the development._](#user-content-fn-1)[^1]

The Auto Score is a sybil-resistant proof-of-personhood scheme designed for individuals with an Auto ID. This framework assigns weights to various types of evidence, allowing users to submit as much evidence as they want. The system then compiles an aggregate score representing the user's "humanness." Unlike many other proof-of-personhood schemes, Auto Score doesn't rely on biometric data. Instead, it considers evidence from multiple verified online identities, such as Google, Apple ID, and World ID.

Users will interact with a GUI to select all the kinds of evidence they would like to submit. For each piece of evidence, the GUI will trigger the relevant web session and the user will sign-in, in which a ZK web session proof protocol will then take place allowing users to prove a claim during any TLS web session while omitting most information. The user’s proof in some way/shape/form would be recorded on-chain and they would receive a Verified Credential stating that they have an Auto Score of X. The Verified Credential would be issued by LetsID, a centralized “due-diligence” server responsible for verifying a user’s aggregate Auto Score and giving a more succinct/quicker version of verification (via a VC).

**Let’s have a look at the real-world example usefulness of Auto Score**

If a user wants to prove their personhood by claiming they have “citizenship”, they would indicate this via the GUI, and then be redirected to some [us.gov](http://us.gov) website. Then, a web session protocol, such as zkPass, would facilitate the retrieval of the necessary data to help construct a ZKP, proving that this person is actually a citizen.

Ultimately, the Auto Score is calculated using various methods that might include the summation of weighted claims, normalization to adjust scores into a standard range, or incorporating additional heuristics to refine accuracy. This scoring process not only supports the functionality of the Auto ID but also enhances the security and utility of digital identities across platforms.

[^1]: 
