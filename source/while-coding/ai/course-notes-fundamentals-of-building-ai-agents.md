# Notes on Fundamentals of Building AI Agents

This course is part of IBM RAG, AI, MCP course:

Course link: https://www.coursera.org/learn/fundamentals-of-building-ai-agents

## system design

- non-ai systems
  - Pre-AI era software is example of this. They have fixed control logic paths, written in form of code. They don't use LLMs or any other AI component.
- Monolithic AI(LLM) systems
  - System uses LLM which is trained on internet data. No other data source. System sends prompt and LLM responds with the data available from the internet
-  Compound AI systems
  - These systems use LLMs and RAGs to add dynamic nature to the non-AI systems. Here, control logic is still fixed but the system leverages LLMs and RAGs to improve the output. For example, `how many paid vacation days I am left with?`. This query is fed into LLM to generate a query for RAG(a set of docs or a db), LLM gives the query and it is fed to RAG, RAG output is taken and fed to LLM, LLM gives back a sentence `XYZ you have 10 vacation days remaining`
  - In this flow, the execution flow is still fixed that LLM always goes to a HR RAG to find answers. It is statically programed. And a single iteration. LLM on its own can't decide what should be the course of action.
  - These are more intelligent but the control flow is still static.
  - Control flow is still programmed, visible and deterministic.
- Agentic AI systems
  - Here LLM decides the control flow. So, it is completely dynamic.
  - Given a problem, LLM breaks it down into small tasks, creates a plan, executes that plan using various tools available. It knows what tools it has available. It decides which one to use and when. 
  - Here since LLM decides course of action, the control flow is not in human control and indeterministic.

## When and not to deploy AI systems

The four-criteria framework for using agents
Before you build or deploy an AI agent, ask yourself the following questions:

1. Is the task ambiguous or predictable?
    Use agents when the task is ambiguous:
    - The decision path is unclear or cannot be mapped in advance
    - Tasks involve exploration, troubleshooting, or creativity
    
    Use workflows when the task is predictable:
    - You can define all rules and outcomes
    - The process follows a clear, repeatable structure

2. Is the value of the task worth the cost?
    AI agents are more expensive to operate due to exploration overhead. They can consume 10 to 100× more tokens than a workflow.
    
    - Strategic planning with high ROI : use agent
    - Basic customer support task : use workflow

3. Does the agent meet minimum capabilities?
    Before launch, test the agent on three to five key skills.
    
    Here are some examples:
    
    - A research agent must identify, filter, and summarize credible sources
    - A coding agent must write, fix, and validate code snippets
    - A customer support agent must classify issues, resolve common queries, and escalate complex cases appropriately
    - A data analysis agent must clean datasets, detect anomalies, and summarize key trends
    
    If the agent fails these tests, scale back or redesign the agent.

4. What happens if the agent makes a mistake?
    Evaluate the answers to these questions
    
    - Can you catch and correct errors quickly? If so, then using an agent might be appropriate.
    - What's the risk if something is missed? Does the consequence of missing the answer affect the customer’s or organization’s well-being or safety?
    - Does the agent include built-in correction or validation tools?
    - Use agents when risk is manageable or reversible.

### Even powerful agents have challenges.

- Reasoning inconsistency: Agents may succeed once but fail on similar tasks
- Unpredictable costs: Resource use can spike depending on complexity
- Tool integration issues: Agents need well-integrated tools and stable APIs

### When not to use agents
There are some situations when agents are not a good solution. Avoid agents for:

- High-volume, low-margin tasks, such as basic chat support
- Real-time applications, such as instant fraud detection
- Zero-error systems, including medical or security decisions
- Heavily regulated industries need deterministic outcomes

