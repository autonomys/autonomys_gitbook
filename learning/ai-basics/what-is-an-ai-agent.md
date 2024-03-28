# What is an AI Agent

In the context of artificial intelligence, an agent refers to an entity that perceives its environment through sensors and acts upon that environment through actuators to achieve certain goals or objectives.

An AI agent can be a software program, a robot, or any other system that exhibits autonomous behavior and decision-making capabilities. The key characteristics of an AI agent can include:

1. Perception: The ability to perceive and interpret the external environment through sensors, such as cameras, microphones, or other types of input devices.
2. Reasoning: The ability to process the perceived information, reason about it, and make decisions based on that reasoning.
3. Action: The ability to take actions or perform tasks that affect the environment through actuators, such as motors, speakers, or other output devices.
4. Goals: AI agents are designed to pursue specific goals or objectives, which guide their decision-making and behavior.
5. Autonomy: AI agents can operate independently, without direct human control or intervention, to achieve their goals.

Let’s compare a typical LLM like ChatGPT4 to an Agent built with the OpenAI API. They would work similarly when asked a simple question requiring a definitive answer, essentially because they “find” the references to it in their training dataset. But, as soon as they’re given a task, or asked a question that can’t be answered without some additional research, the difference becomes more clear. Imagine you’ve asked the GPT and your Agent how to fix world hunger. GPT is likely going to provide the most common answer available on the web statistically when an Agentic AI might have another approach. It would start self-prompting some additional questions: does the hunger reasoning in the new world have the same underlying reasoning compared to the countries located in the old world? It could use the internet to check if there are any recent events, like wars or pandemics which affected the state of hunger in the world. After doing some initial research, it would try to find a solution for each specific group of people and combine them all in one complete response.

As you can see from the example above, the AI Agent is one step closer to AGI compared to LLM, due to its ability to self-prompt, use other available tools like the internet, other LLMs, and sometimes a database to deepen the knowledge on a subject before providing an answer. AI agents can analyze the surroundings and context, reason about available information, and take action to maximize their chances of success. Unlike transformers, which are specialized for processing text, AI agents have a broader range of applications, including robotics, gaming, virtual assistants, and autonomous vehicles.

In the example above we mention that the AI agent was built with an OpenAI API - which is another key difference between agentic AIs and a typical chatbot style LLM. The more complicated the task is, the more models and tools the Agent would require to use to solve them, and the communication between them is happening through API calls. We see a future where agents become increasingly autonomous - they no longer require detailed, step-by-step instructions from the person and can decide themselves what API or even another agent to create or query to get the job done. Perhaps, most of the users of those APIs and the internet itself won’t be people in the future, rather agents working on behalf of people!

To wrap it up: while LLMs exhibit remarkable capabilities in language-related tasks, AI agents demonstrate versatility and adaptability in diverse real-world scenarios, where achieving desired outcomes through creative solutions is crucial.
