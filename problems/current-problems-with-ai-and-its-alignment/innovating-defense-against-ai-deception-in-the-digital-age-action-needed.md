---
description: Feels out of place, some duplication with articles around
---

# Innovating Defense Against AI Deception in the Digital Age (action needed)

In world without a a simple, distributed, interoperable open standard to identify AI agents (and authenticate the content they produce on behalf of humans or AI providers), social platforms find it virtually impossible to enable any kill switch or safety lever to stop con artists from producing AI-based deepfake videos of celebrities and political candidates. Reputations and democracy remain continuously under threat.

![deepfake.jpg](https://prod-files-secure.s3.us-west-2.amazonaws.com/562415b3-26fd-44e9-a7cf-40b1a8253627/341bf30a-8c8f-4d37-be29-81758c1f8c01/deepfake.jpg)

**Automated Detection of AI Generated Content**

Auto ID provides a framework for detecting AI-generated content, allowing platforms and providers to trace and potentially mitigate malicious use by marking content with a unique identifier and facilitating the tracking of its origin, even in cases of altered content.

**How?**

🕵️‍♂️ Auto ID offers a mechanism to trace AI-generated content back to its source, potentially identifying malicious users and the AI provider.

📰 If a bad actor uses an AI provider to create and disseminate fake news and deepfake images on X, aiming to spread disinformation. But because the AI provider issues surrogate Auto IDs for each user, tied to their AI model usage, it tracks content generation and authenticity.

🔍 Thus, every piece of content generated through the AI provider is marked with a semantic hash, stored for fast provenance verification via a public API.

🚩 X implements a content verification process using the AI provider’s API, flagging content that matches known AI-generated hashes with a distinct icon to warn users.

📢 When potentially malicious AI-generated content is detected, X can notify the AI provider, leading to internal review and possible action against the user.

💡 Even with modifications to AI-generated content, semantic hashing techniques can still accurately identify and flag it due to their ability to detect near matches.
