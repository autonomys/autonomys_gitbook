---
description: An overview of Autonomys' interface for accessing the DSN
---

# Auto Drive

**Auto Drive** is a decentralized content-addressed storage solution built on the Autonomys Network.

Auto Drive transforms the underlying blockspace that forms the foundation of Autonomys’ distributed storage network (DSN) into a secure, easy-to-use, interoperable data storage tool with a user experience akin to Web2 cloud platforms.

## Key features

* **True On-chain Storage**: Unlike other "decentralized" storage solutions that often simply distribute data across servers, Auto Drive provides access to genuine on-chain blockspace. This means your data inherits the same permanence, security, and decentralization guarantees as the Autonomys Network itself.
* **User-Friendly Dashboard**: Auto Drive offers an intuitive web interface at [ai3.storage](https://ai3.storage/) that makes storing and accessing blockspace as simple as using a traditional cloud storage service. Users can drag and drop files, create directories, and manage their stored data with ease.
* **End-to-End Encryption Options**: Security is paramount in the decentralized ecosystem. Auto Drive provides optional end-to-end encryption, giving flexibility that puts you in complete control of your data security while maintaining the benefits of on-chain blockspace.
* **Developer-Friendly SDK and API**: For developers looking to integrate blockspace into their applications, Auto Drive offers:
  * A comprehensive TypeScript/JavaScript SDK via [@autonomys/auto-drive](https://github.com/autonomys/auto-sdk/tree/main/packages/auto-drive)
  * A RESTful API with complete documentation
  * Familiar interfaces that make integration straightforward
* **Scalable Data Structure:** Auto Drive utilizes the Auto-DAG (Directed Acyclic Graph) data structure, which breaks down larger files into manageable chunks that fit within the network's blockspace. This approach ensures:
  * Data integrity through cryptographic verification
  * Efficient storage and retrieval
  * The ability to store files of any size within the available blockspace

## **Why Auto Drive?**

Today's Web3 ecosystem faces a significant contradiction: while blockchain transactions themselves are immutable and decentralized, the actual data referenced by those transactions is often stored on centralized or temporary infrastructure, creating critical reliability issues. This is because traditional blockchain networks and storage solutions treat data storage as a separate service—either on-chain at enormous cost or off-chain with compromised security.

In the Autonomys Network, storage is an intrinsic byproduct of the network's consensus mechanism—Proof-of-Archival-Storage (PoAS)—which naturally generates vast amounts of blockspace. Auto Drive makes this blockspace accessible to developers and users. Data stored via Auto Drive is secured by the network’s consensus and permanently stored in the same blockspace that maintains the Autonomys Network’s own history and state.

## **Getting Started with Auto Drive**

Ready to experience truly on-chain blockspace at practical prices? Here's how to get started:

1. **Auto Drive Dashboard**: Visit [ai3.storage](https://ai3.storage/) and sign in with your preferred authentication method
2. **Developer Integration**: Install the SDK with `npm install @autonomys/auto-drive` or `yarn add @autonomys/auto-drive`
3. **API Access**: Create API keys on the Auto Drive Dashboard to access the full functionality programmatically

## Resources

* [Autonomys Developer Hub (Auto Drive)](http://develop.autonomys.xyz/sdk/auto-drive) — Get started with Auto Drive
* [Auto Drive Dashboard](https://ai3.storage/) — Web app for uploading, downloading and sharing files & folders, and creating API keys for the Auto SDK
* [Auto Drive Gateway](https://gateway.autonomys.xyz/) — Unified interface for accessing files & folders stored on Autonomys' mainnet and Taurus testnet
* [Auto Drive API docs](https://mainnet.auto-drive.autonomys.xyz/api/docs) — Available function signatures
* [Auto SDK (Auto Drive)](https://github.com/autonomys/auto-sdk/tree/main/packages/auto-drive)
* [Auto Drive Repository](https://github.com/autonomys/auto-drive)
