# Personal AI

In the previous articles we briefly covered what an LLM is, how development of transformers were essential to the tools that we use today and discussed the current trend of Agentic AI which aims to use AI in a more meaningful and sometimes creative way. But there’s more to it! Imagine if the agent wasn’t only using the publicly available information about the world and it’s training dataset, but was able to know more about you, your set of rules and beliefs, your background and your opinions about anything and provide a unique answer which was aligned with your view of the world. That is exactly what Personal Agentic AI is.

Here are some first attempts to popularize personal AI agents:

* [Rabbit R1](https://www.rabbit.tech/keynote) compact personal AI assistant portable device
* [Langchain](https://www.langchain.com/agents) is the leading tool for [building agents](https://python.langchain.com/docs/modules/agents/) using models like GPT-4 through the Open AI API. They have lots of [articles](https://blog.langchain.dev/planning-agents/) on their [blog](https://blog.langchain.dev/) and many webinars describing how this works.
* OpenAI recently published [Practices for Governing Agentic AI systems](https://openai.com/research/practices-for-governing-agentic-ai-systems) to explain the dangers and risks of agents. ChatGPT is partially agentic. GPTs and Open AI [assistants](https://platform.openai.com/docs/assistants/overview) both allow for developing semi-agentic AI.
* Popular movie [Her](https://en.wikipedia.org/wiki/Her\_\(film\)) shows well what a personal AI agent that starts as AGI and becomes ASI would look like.
* [PersonalAI](https://www.youtube.com/watch?v=SLgo4fRQjzM) which essentially creates your digital twin, with representation of your memory (Memory Stack) and your personal talking style (Personal Language Model), that chats with your friends instead of you.

## **Agent Decision-Making and Planning**

From managing your investments to meal planning for your family, your personal AI agent juggles a myriad of tasks and objectives. To make optimal decisions aligning with your long-term goals and priorities, it employs advanced decision-making and planning strategies.

Using decision-theoretic models, your agent evaluates the potential outcomes and ripple effects of each possible course of action when arranging your day. It weighs factors like your schedule constraints, health tracking data, traffic predictions, and even your latest emotional state readings. With techniques like [Monte Carlo tree search](https://en.wikipedia.org/wiki/Monte\_Carlo\_tree\_search), it rapidly simulates millions of branching future scenarios to plot out ideal schedules and plans.

In domains lacking full predictability, like negotiating major purchases or fielding open-ended queries, your AI leverages game theory and reinforcement learning. It constructs models of the other agents' behaviors and updates its own response strategies based on their actions and your feedback, continually learning to make better decisions tailored just for you.

## **Agent Learning**

What makes your personal AI agent truly remarkable is its ability to continuously learn, adapt, and grow more personalized with each interaction and new experience. It's an ever-evolving repository of your preferences, habits, and idiosyncrasies.

Through supervised learning on all your past data, from emails and documents to calendar events and GPS traces, your agent builds rich predictive models of your behavior and patterns. It learns to automate routine tasks while also identifying anomalies worthy of your attention.

But your AI goes beyond following rules - it observes the real-world outcomes and your feedback to refine its behavior through reinforcement learning. If you override a scheduling decision, it learns. If you express dissatisfaction with a suggestion, it course-corrects its strategy.

Moreover, by processing natural conversations through unsupervised learning, your AI agent bootstraps its own conceptual understanding to provide more intelligent and nuanced responses. Over time, it develops an emergent model of you as a unique individual - your traits, idiosyncrasies, and the very essence of how you think. In essence, it becomes an extension of your own cognition and identity.
