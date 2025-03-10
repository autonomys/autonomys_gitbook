---
description: An overview of the cryptographic primitives used by the Subspace Protocol
---

# Proof-of-Archival-Storage (PoAS)

## Hashing

Hashing provides succinct commitments to arbitrary data (blocks, transactions, etc.) that are deterministic, verifiable and cannot feasibly be reversed. The Subspace Protocol uses the BLAKE2b-256 and BLAKE3 hash functions in different places.

## Digital signatures

Digital signature schemes secure different parts of consensus by providing a means of authentication. We currently use Schnorr/Ristretto x25519 (also known as sr25519) as the key derivation and signing algorithm (part of the [schnorrkel](https://github.com/w3f/schnorrkel) library):

* Non-canonical Schnorr signatures are used to sign rewards for a newly forged block (as defined in Substrate) and votes by farmers, as well as transactions and transaction bundles by domain operators.
* Canonical (deterministic) signatures are used as a verifiable random function (VRF) in the slot leader election among domain operators. A canonical scheme is necessary for these cases to prevent attackers from repeatedly signing until they produce an election solution that meets the threshold (as part of a grinding attack).

## Erasure coding

An erasure code extends any given data such that the full original data can be recovered from a subset and is protected against loss. The Subspace Protocol uses erasure coding to encode and decode blockchain history pieces and their KZG commitments in an archived segment, allowing for the distributed storage of pieces across farmers, and protecting the data against loss in the event of any failures or network partitions. Erasure code is also used in plotting—together with proofs-of-space—to create unique, easily recoverable plot files for each farmer. We currently use a Discrete Fourier Transform-based systematic Reed-Solomon code with a rate of 1/2 over the field 𝐹𝑟, where 𝑟 is the [size of the subgroup of points](https://hackmd.io/@benjaminion/bls12-381#Curve-equation-and-parameters) on the BLS12-381 curve for the piece chunks, and the same approach over the subgroup of elliptic curve points $$G_1$$ for piece commitments.

## Kate-Zaverucha-Goldberg (KZG) polynomial commitments

KZG polynomial commitment schemes allow for _constant_-sized inclusion proofs for arbitrary-sized data sets, specifically:

* The commitment size is _constant_ and equal to one elliptic curve point of an elliptic curve group that admits pairings.
* The witness size is _constant_ and equal to one curve point.
* Verification time is _constant_ and requires two point-scalar multiplications and two pairings regardless of the size of the committed data set.
* Proving time (commitment and witness generation) is _linear_ in the size of committed data. The Subspace Protocol uses BLS12-381, which has 48 bytes for elliptic curve points (commitments and witnesses) serialized in compressed form.

The protocol uses the KZG commitment scheme to commit to the archived pieces of history and segments of pieces so farmers storing pieces in their plots can always succinctly prove that a particular piece is a valid part of the blockchain history, and clients who request pieces can verify the proofs efficiently. The synergy between KZG and Reed-Solomon erasure code allows us to have:

* succinct commitments to data of arbitrary size
* succinct witness of the inclusion of data fragments in the blockchain history
* efficient verification
* provably correct erasure coding

KZG requires a one-time trusted setup of the universal reference values (public parameters). In the spirit of interoperability, the Subspace Protocol uses the same reference values as Ethereum, as computed during a distributed multi-party computation ceremony held by the Ethereum Foundation. This permits cross-chain compatibility of KZG proofs between Autonomys and Ethereum.

## Merkle trees

Merkle trees provide succinct commitments (Merkle roots) to arbitrary-sized data sets with efficient _logarithmic_-sized inclusion proofs. The Subspace Protocol uses Merkle trees for:

* extrinsics sets in blocks (as defined in the Substrate framework)
* the state of the blockchain (as defined in the Substrate framework)
* execution traces for domain blocks

## Encoding mapping

Encoding provides a means to make useful data (i.e. chunks of blockchain history) look like random data, while allowing for the retrieval of the useful data through decoding. The Subspace Protocol uses simple XOR as an encoding function.
