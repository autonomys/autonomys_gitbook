---
description: >-
  This page is still being designed and be updated as soon as there is more
  information available.
---

# AutoKit features highlights

## Auto SDK Design

The main goal of Auto Kit is to create, verify, and revoke Auto ID (digital identity). As the list of supported features Auto ID expands, Auto Kit will assist in calculating functionality to calculate the Human score - the unique metrics to determine a human from AI online.

The initial implementation will be done in Python. For a prototype implementation see [this GitHub repo.](https://github.com/subspace/auto-kit)

### Auto ID Identity

* Self-issue
* Issue to another entity
  * Create CSR
  * Sign CSR
* Register Auto ID
* Verify Auto ID registration

### Auto ID Authentication

* Sign data
* Verify signature
* Mutual authentication - mTLS
* Associate provable identity claims with an entity
  * OIDC ID tokens

### Auto ID Authorization

* Delegate claim to entity
* Delegate OAuth claim to entity
  * Manage refresh tokens
