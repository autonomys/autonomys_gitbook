---
description: Do we need this one in general?
---

# AI Worms (action needed)

As autonomous agents assume a greater role in internet-based tasks, AI worms emerge as a new concern, [with a recent study](https://www.wired.com/story/here-come-the-ai-worms/) shedding light on this development.

The study focuses on the creation of innovative generative AI worms capable of migrating across systems, posing threats such as data theft or malware deployment. Named MORRIS2, this worm, devised by a team of researchers compromises a generative AI email assistant, facilitating the extraction of data from emails and the dissemination of spam.

This experiment took place within a controlled environment, targeting no publicly accessible email assistants. Nevertheless, it underscores the potential security vulnerabilities associated with language models evolving into multi-modal entities. The researchers employ an adversarial self-replicating prompt. The prompt operates under a guise, engaging the AI assistant in a role-playing scenario where it must replicate certain text, defined by start and end characters, twice within an email. This cleverly engineered logic ensures the perpetuation of the prompt's segment, thereby enabling its recognition and execution by subsequent language models. The payload embedded between these characters may contain commands to share sensitive information, such as email addresses and phone numbers, to a specified recipient.

Preserving trust in AI agents requires a method to distinguish among various autonomous entities online. Adopting a universal, federated identity standard for agents, along with a framework for authenticating and authorizing them, allows for easier exposure of AI worms. In an AI environment where participants opt for a simple, interoperable open standard identity, eliminating the need to construct their own and then create bridges and adaptors to other identity frameworks, they effectively contribute their trust model to the system.