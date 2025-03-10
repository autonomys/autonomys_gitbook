---
description: An overview of Autonomys' networking protocols
---

# Networking Protocols

Based on [libp2p](https://libp2p.io/), Autonomys' networking stack implements several unique protocols to handle a variety of essential tasks.

## Transaction propagation

Autonomys uses a gossip mechanism to propagate transactions to peers across the network, ensuring nodes have a consistent view of unconfirmed transactions. When a node receives a new transaction, it validates the transaction and, if valid, adds it to its transaction pool, before broadcasting it to its directly connected peers.

When a connected peer receives the transaction, they too validate it, retaining a copy (if valid), before sharing it with all their connected peers (excluding the one from which it was received). Consequently, the transaction disseminates from its source, spreading throughout the network, ensuring every node receives a copy.

## Block and bundle relay

Autonomys introduces 'compact blocks' and 'compact bundles' relayed via gossiping to propagate new blocks and bundles across the network as efficiently as possible. As a substantial part of each block's size is the body of transactions included within it, and each transaction has previously been broadcast to nodes, rebroadcasting the entire body is unnecessary. As such, when a node receives a new block, it validates the block header and transactions, and if valid, builds a compact block message containing only the block header and transaction IDs that is then gossiped across the network.

When a connected peer receives the compact block, it verifies it has all the referenced transactions in its pool, requesting the complete transactions from the broadcasting node if any transactions are missing. This optimization allows for fast block propagation while minimizing unnecessary transaction data transfer across the network. A similar mechanism is used for bundle relay, where a compact bundle contains only the bundle header and transaction IDs, allowing for rapid dissemination of new bundles throughout the network.

## Synchronization

Autonomys employs an adaptive synchronization protocol to sync nodes to the latest state of the network efficiently. This adaptive protocol chooses between DSN sync and block sync based on how far the node is behind the blockchain.

The distributed storage network (DSN) sync uses a specialized synchronization protocol enabled by Autonomys' unique archival and storage mechanism. The DSN sync is attempted every time a node joins the network or detects it is more than a hundred blocks behind the live network. The node first gathers information from its peers about the latest archived segment headers to verify whether any new data has been archived since it last synced. If new segments are available, it then downloads the headers, and verifies whether they form a chain. Once verified, it downloads the complete segment data from the DSN, verifies commitments, and locally reconstructs blocks from pieces.

The DSN sync allows a node to sync hundreds or thousands of blocks at once by downloading archived data directly from the DSN (rather than fetching individual blocks from peers). Once a node has downloaded all missing segments and imported the archived history, it switches to syncing recent blocks from other nodes until it reaches the end of the blockchain, at which point it is live.

## Piece retrieval

Autonomys implements a piece retrieval protocol that allows nodes to retrieve history pieces from the network in the most efficient way possible. When nodes need pieces for plotting, or when requested by a client application, they send requests to peers with IDs close to the required piece index hashes. With a high probability, the peers receiving the requests will have the pieces available in their piece caches and can respond with the piece data. In the rare case none of the peers have the required pieces, the request falls back to asking them to decode the pieces from their plots.
