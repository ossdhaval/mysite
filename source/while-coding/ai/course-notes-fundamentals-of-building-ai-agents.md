# Notes on Fundamentals of Building AI Agents

This course is part of IBM RAG, AI, MCP course:

Course link: https://www.coursera.org/learn/fundamentals-of-building-ai-agents

## system design

- non-ai systems
  - Pre-AI era software is example of this. They have fixed control logic paths, written in form of code. They don't use LLMs or any other AI component.
- AI systems or compound AI systems
  - These systems use LLMs and RAGs to add dynamic nature to the non-AI systems. Here, control logic is still fixed but the system leverages LLMs and RAGs to improve the output. For example, `how many paid vacation days I am left with?`. This query is fed into LLM to generate a query for RAG(a set of docs or a db), LLM gives the query and it is fed to RAG, RAG output is taken and fed to LLM, LLM gives back a sentence `XYZ you have 10 vacation days remaining`.
  - In this flow, the execution flow is still fixed that LLM always goes to a HR RAG to find answers. It is statically programed. And a single iteration. LLM on its own can't decide what should be the course of action.
  - These are more intelligent but the control flow is still static.
  - Control flow is still programmed, visible and deterministic.
- Agentic AI systems
  - Here LLM decides the control flow. It knows what tools it has available. It decides which one to use and when. Given a problem, LLM breaks it down into small tasks, creates a plan, executes that plan using various tools available.
  - Here since LLM decides course of action, the control flow is not in human control and indeterministic.
