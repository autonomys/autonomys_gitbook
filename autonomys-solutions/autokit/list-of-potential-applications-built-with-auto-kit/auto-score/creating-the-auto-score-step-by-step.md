# Creating the Auto Score step by step

The calculation of Auto Score for each entity with Auto ID will consist of multiple steps:

**External Registration — Step 0**: Many users maintain multiple online identifiers, spanning from their Google username to their Apple ID, World ID, and more. These platforms can verify various user attributes such as email or phone number validity, and in the case of World ID, successful retina scan completion. These verified attributes, known as identity claims, may indicate aspects of humanness, for example, a verified phone number/email or even retina scan. However, they are currently dispersed across different providers. Autonomys aims to consolidate these claims under a unified Auto ID.

**Auto ID Registration — Step 1:** Users require a central identifier to aggregate all their claims. This identifier, in our case, will be Auto ID; it will also serve as the foundation for various other functionalities besides an Auto score. In essence, users must register an Auto ID, if they haven't already, to incorporate their external claims and eventually obtain an Auto score

**Registering an OIDC Claim — Step 2:** Google and World ID, as OIDC providers, utilize the OIDC interface to transmit identity claims to other parties. Autonomys will implement its own backend server to function as the client application. Autonomys will also offer a frontend for querying this server.

Here is an example flow. The user, through the Auto front-end, indicates a preferred OIDC Provider to the Auto back-end server, and their public identifier (ie Auto ID). The Auto back-end server, already having integrated with the OIDC Provider and obtaining any necessary authentication credentials, redirects the user to the OIDC Provider. The user inputs their OIDC credentials (eg Google username) into the OIDC Provider’s front-end. After the OIDC Provider’s back-end authenticates the credentials, it will send a signed token to the Auto back-end server.

Unfortunately, this means that the Auto back-end server will learn about user’s OIDC identifiers and claims. However, the team is currently thinking of some kind of combination of zero-knowledge proof and blind signatures in order to keep anonymity.

**Auto Score Calculation — Step 3:** Depending on the implementation of step 2, the Auto Score calculation would occur either visibly in step 3 or anonymously in step 4. In the latter case, for step 3, a service would prompt the user to authenticate their Auto Score, in which the Auto score would be anonymously proved in step 4.

Nonetheless, the calculation method could be any of the following. Of course, anything besides a simple summation would become dramatically more difficult to implement in a zero knowledge proof.

* summation of weights: Assume every proof-of-personhood registry or claim linked to an identifier has a certain weight. These weights, per user, can then be summed to represent her score. For example, if Alice is a) registered with WorldID and has a US state drivers license, b) this information is included on the Subspace registry and c) WorldID has weight 8 and the drivers license has weight 2, then Alice’s ‘human score’ is 10.
* normalization method: We can use the previous approach, and then divide the sum by the max possible sum and multiply by 100. This will give each person’s score as a percentage
* additional heuristics: We could always use the above methods with additional heuristics. For example, we could categorize each kind of claim into a category of evidence (ie retina scan, facial scan, passport, etc). Then, we could limit users to only getting a score per category, and summing up the weights of the different categories.

This is not a finalized process yet and we’re still researching more ideas on making the progress smooth from the user perspective but simultaneously keeping it thorough to ensure the consistent and confident division between human and AI entities or organizations.
