# Public Key Infrastructure

#### Public Key Infrastructure & Transport Layer Security

Public Key Infrastructure (PKI) is like a special club that websites need to join to prove they are legitimate and not trying to trick you. When a website wants to join the club, they get a membership card called a "digital certificate" from the club leader called a Certificate Authority (CA). This certificate has a secret code called a public key that only the real website knows.

When you visit a website, your web browser checks if they have a valid membership card or certificate from the club. If they do, it means you can trust and safely share private information with the website. It's like showing up to a friend's house and checking their ID to make sure they live there before going inside.\
\
PKI also consists of Registration Authorities (RAs) that verify the identity of entities requesting a certificate before the CA issues it. There are repositories for storing and retrieving certificates as well as Certificate Revocation Lists (CRLs), which are essential for maintaining the integrity of the system by listing certificates that are no longer trusted.\
\
\
**Transport Layer Security (TLS)**

Transport Layer Security (TLS) is a secret code language that your computer and a website use when talking over the internet. It scrambles up your conversation into an encrypted message that bad people can't understand if they try to snoop. TLS uses those membership cards or certificates from PKI to make sure your computer is really talking to the correct website through a process called authentication.

It's like you and your friend making up a silly code language that only you two understand. That way, if someone tried to listen to your conversations, it would just sound like gibberish to them. Showing the PKI certificate proves you're talking to the right friend. The encrypted conversation using TLS is like the code language.\
\
TLS almost works as a "handshake", where the server and client exchange keys, negotiate encryption algorithms, and verify each other's certificates. This process ensures that the communication channel is secure before any data is exchanged.

<figure><img src="../../.gitbook/assets/education-center-public-key-infrastructure.jpg" alt=""><figcaption></figcaption></figure>

