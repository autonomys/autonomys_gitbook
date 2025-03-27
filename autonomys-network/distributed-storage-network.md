---
description: >-
  An overview of the structure and features of Autonomys' distributed storage
  network
---

# Distributed Storage Network (DSN)

Autonomys Network chain data is distributed to [farmers](../auto-suite/spaceacres-cli/farmers.md) for storing and serving as pieces of the blockchain history via our distributed storage network (DSN). Autonomys introduces a DSN to ensure all chain data is permanently stored in a load-balanced, fault-tolerant, and efficiently recoverable manner across all farmers (no matter how large it grows), and the consistency of storage over time, given the heterogeneous storage capabilities of farmers. Our DSN design guarantees the following properties:

* _Permissionlessness_: The system operates without central coordination, accounting for dynamic farmer availability and non-uniform growth of historical data over time.
* _Retrievability_: Both full and single-piece retrieval are facilitated, with requests balanced evenly across all farmers, ensuring that the overhead of serving history remains negligible.
* _Verifiability_: Farmers are not required to synchronize or retain the full history, yet the system remains efficiently verifiable.
* _Durability_: The probability of any single piece being lost, whether through accidental or malicious means, is minimized.
* _Uniformity_: On average, each piece is stored an equal number of times across the network.

These features enable the historical data to expand beyond the storage capacity of any individual farmer, while allowing farmers to allocate storage resources according to their individual capabilities.

The Autonomys Network DSN is comprised of multiple distinct layers that together serve historical data pieces to requesting [nodes](nodes.md), with each layer contributing to different aspects of data availability, durability and efficient retrievability. This multi-layered approach was developed to balance security and performance, and interestingly, bears similarities to other recent data availability solutions developed independently from our approach, such as [Tiramisu](https://doi.org/10.48550/arXiv.2308.07163).

<figure><img src="../.gitbook/assets/infographic_cache-layers (1).png" alt=""><figcaption><p>Distributed Storage Network</p></figcaption></figure>

## Developers

Developer documentation for building on the DSN is available on the [Autonomys Developer Hub](https://develop.autonomys.xyz/).&#x20;

Auto Drive API documentation is available [here](https://mainnet.auto-drive.autonomys.xyz/api/docs).

## (L3) Content delivery network (CDN)

The topmost layer of our DSN is a content delivery network (CDN) designed for optimal performance under optimistic network conditions. The CDN layer (operated by a large permissioned network of nodes) significantly enhances retrieval speed and provides robust performance under normal network conditions. This layer provides web2-like performance for data retrieval:

* Farmers upload newly created pieces to the CDN.
* Nodes can quickly retrieve pieces from the CDN (similar to downloading from a web2 streaming service).
* The CDN serves as an ultra-fast channel for passing messages between nodes, facilitating the rapid collection of data pieces.

## (L2) Pieces cache

The pieces cache layer is designed to facilitate efficient piece retrieval for data reconstruction and farming. Its primary function is to minimize retrieval latency. While retrieval from archival storage necessitates computationally intensive decoding by farmers—taking approximately 1 second on consumer hardware—L2 retrieval is near-instantaneous due to the storage of unencoded pieces in the disk cache.

The L2 cache utilizes a distributed hash table (DHT) to store pieces based on the proximity of the piece index hash to the peer ID. Farmers, being the most suitable candidates for L2 storage, allocate a small percentage of their pledged storage for this purpose. The overall storage network replication factor determines the number of farmers storing each piece.

The piece cache layer population process is as follows:

1. Nodes generate new segments of pieces during the archiving process.
2. These new segments are temporarily stored in the node’s cache.
3. Farmers receive the newly archived segment index from the latest block header.
4. Farmers compute the piece index hashes within the segment and determine which pieces to pull to their L2 based on hash proximity to their peer ID.
5. Relevant pieces are then pulled to the farmer’s local L2 cache.

In the rare case that a specific piece cannot be retrieved to the L2 cache, the farmer will attempt to decode the required piece by requesting its neighboring pieces by index and erasure decoding it from that set. If this fails, the farmer will next attempt L1 retrieval.

## (L1) Archival storage

The archival storage layer is the fundamental layer responsible for the permanent storage and durability of all chain data. It comprises all storage pledged by farmers for storing encoded pieces of chain history, also known as plots. This layer provides the highest level of security against powerful adversaries, albeit at the cost of performance.

Functioning as ‘cold storage’, the archival storage layer ensures the availability of history pieces in the rare event of an L2 cache miss. However, retrieval from archival storage is resource-intensive and time-consuming; thus, it is utilized only when L2 retrieval fails. Typically, the L1 layer of farmers is populated with pieces received from L2.

The archival storage layer population process is as follows:

1. The farmer decides how much storage to allocate to the network.
2. Based on the amount of storage pledged, the farmer pseudorandomly and verifiably selects enough pieces of history to fill that space.
3. The farmer pulls the selected pieces from the L2 or L1 of other farmers.
4. The farmer masks the pieces as described in the plotting protocol.
5. Every time a new segment is archived, the farmer runs a check to see whether they need to replace any pieces.

The last step is necessary to ensure that new history gets replicated uniformly across many farmers in the network, regardless of how long they have been participating in the network or how long ago they initialized their plots. This plot expiration is set up such that the farmer gradually replaces subsets of pieces in the plot as the history of the chain grows. On average, by the time the history has doubled in size, as compared to when the plot was initialized, half of the farmer’s plot will have expired and been replotted. By the time the history quadruples, the farmer will have replotted their whole plot once over. The choice of gradual expiration instead of full farm replots ensures maximum uptime of the farmers’ archival storage layer for serving pieces to the DSN.

## Cache types

Separately from the above cache layers, we distinguish the following types of cache:

* _Node cache_: Contains newly created pieces from the most recent archived segments. It is limited to a few recent segments and progressively replaces older pieces with new data.
* _Farmer cache_: Contains pieces in the L2 cache, automatically populated upon receipt of new archived segment announcements. Pieces are cached according to their proximity to the farmer’s peer ID.
* _Object cache_: Contains recent and popular user-uploaded objects and their mappings to pieces.

To incentivize the farmer network to maintain the desired replication factor for historical data, Autonomys implements a novel algorithm that dynamically adjusts the cost of on-chain storage, or _blockspace_, in response to fluctuations in storage supply and demand.
