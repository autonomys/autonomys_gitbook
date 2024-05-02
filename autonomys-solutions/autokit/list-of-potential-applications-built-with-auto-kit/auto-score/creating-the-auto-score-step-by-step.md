---
description: >-
  This is an early outline of Auto Score. The steps and providers references
  below might and likely be changed or adjustment during the development.
---

# Creating an Auto Score Step by Step

## Calculating Auto Score

The Auto Score is a unified metric calculated for individuals who have an Auto ID, integrating various verified attributes from multiple online identities such as Google, Apple ID, and World ID. This score is derived from identity claims which could range from simple email verifications to complex biometric data like retina scans. The aim is to centralize these disparate claims into one identity—Auto ID—to facilitate various functionalities including a reliable score of "humanness."

To achieve this, Autonomys employs a system that uses OpenID Connect (OIDC) providers to securely transfer identity claims to an Auto ID. This method ensures that while users consolidate their identity attributes from different platforms, their privacy is safeguarded through advanced technologies like zero-knowledge proofs and blind signatures. These technologies are designed to verify the claims without compromising the anonymity of the user.

Ultimately, the Auto Score is calculated using various methods that might include the summation of weighted claims, normalization to adjust scores into a standard range, or incorporating additional heuristics to refine accuracy. This scoring process not only supports the functionality of the Auto ID but also enhances the security and utility of digital identities across platforms.
