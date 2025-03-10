---
description: The first phase of the Subspace Protocol
---

# Archiving

**Archiving** transforms the chain blocks at a configured depth (currently 100 blocks) from the end of the chain into a canonical history ready to be distributed to farmers for storage.

Our archiving construction is primarily based on the paper '[_Information Dispersal with Provable Retrievability for Rollups_](https://eprint.iacr.org/2021/1544)**'** from the Tse Lab at Stanford University. The key ideas we inherit from this paper are viewing the data to be archived as a matrix, and taking a “1.5D approach” with column-wise erasure coding and row-wise KZG commitment. Combining the polynomial nature of the Reed-Solomon erasure code and KZG with the homomorphic properties of KZG guarantees the consistency, retrievability, and efficient verifiability of the archived data.

## Background

When a block reaches archiving depth, its contents are added to a raw chain history buffer. The buffer is then sliced into _records_.

* A _record_ of blockchain history is a vector of $$2^{15}$$ chunks.
* A _chunk_ is the smallest unit of data measurement (254 bits, rounded to 32 bytes by padding with 0 for convenience) and a field element for KZG.
* A _piece_ is a record concatenated with a KZG commitment and a witness of inclusion in a specific segment.

The archiving process produces segments of pieces.

<figure><picture><source srcset="../../../.gitbook/assets/Piece-dark.svg" media="(prefers-color-scheme: dark)"><img src="../../../.gitbook/assets/image (13).png" alt=""></picture><figcaption><p>Archived piece</p></figcaption></figure>

## Workflow

The blockchain history data is archived when it reaches the archiving depth to avoid forks and reorganizations. The Subspace Protocol begins archives 128MiB segments of raw blockchain history when there are enough blocks at the current archiving depth to fill a segment, as follows:

1. Slice the recorded history segment into 128 source records and stack them into a matrix (so each row is a record).
2. Commit to chunks of each source record (each row) under the KZG vector commitment scheme.
3. Erasure code each column by interpolating a polynomial over the source record chunks in that column and evaluating the polynomial on twice as many points. As a result, the matrix now has twice as many rows—256—and consists of 128 source and 128 extended (parity) records.
4. Erasure code the source record commitments similarly by interpolating a polynomial over the source record commitments in that column and evaluating the polynomial on twice as many points. This allows us to show that the erasure coding of data was performed correctly with the homomorphic property of Reed-Solomon erasure code and KZG. As a result, the extended commitments (yellow boxes in the diagram) obtained by erasure coding the source commitments are the same as if we were to commit to the extended rows.

<figure><img src="../../../.gitbook/assets/infographic_archived-segment (1) (1).png" alt=""><figcaption><p>Archived segment</p></figcaption></figure>

5. To tie the 256 records and 256 commitments to those records together into a segment, commit to the record commitments, and obtain the segment commitment.
6. Compute a witness for each record commitment inclusion in the segment commitment. With this two-tier commitment, we can later show that a given chunk belongs to a specific record and that record belongs to an archived segment and, thus, to the canonical history of the chain.
7. Build 256 pieces, where each piece consists of a 1MiB record, a 48-byte commitment to record data, and a 48-byte witness of inclusion in a segment.
8. Append the new pieces to the canonical history and store the segment commitment in the chain state. The segment commitment is also included in the successive segment to link back to the last segment and form the chain of segments that represent the canonical history of the blockchain.

Once a segment has been archived and the pieces are ready for the farmers to store, the next phase is [plotting](plotting.md).
