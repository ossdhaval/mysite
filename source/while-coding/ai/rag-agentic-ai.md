Course:

https://www.coursera.org/professional-certificates/ibm-rag-and-agentic-ai

Best agentic ai framework:
https://blog.jetbrains.com/pycharm/2026/06/top-agentic-frameworks-for-building-applications-2026/

# Notes

## How do the A2A, MCP, and AP2 protocols work together for agentic commercial transactions?
The A2A, MCP, and AP2 protocols work together to form the framework of agentic commercial transactions.

To understand how these three protocols work together in agentic commercial transactions, let's look at a simple example:

User request: "Order me a new pair of wireless headphones with noise cancellation, under $250."
A2A at work: The shopping agent communicates with a retailer's product agent and a payment service agent to manage the process.
MCP at work: The agent gathers product details, user preferences, and past purchase history via the Model Context Protocol.
AP2 at work: After selecting a suitable product, the agent creates a Cart Mandate. Once the user reviews and approves it, the payment agent securely processes the transaction.

## What the Adapter Does
The langchain-mcp-adapters library bridges this gap by:

- Wrapping MCP tools as LangChain BaseTool instances — so the ReAct agent can discover and call them like any normal LangChain tool.
- Translating invocations — when the agent calls a tool, the adapter converts the call into a proper MCP tools/call JSON-RPC request sent over the MCP transport.
- Unwrapping results — it converts MCP's content block arrays back into plain strings/values the agent's message history understands.
- Managing the MCP session lifecycle — connecting to the MCP server (via stdio/SSE), handling the initialize handshake, and keeping the session alive across tool calls.

- <img width="388" height="628" alt="image" src="https://github.com/user-attachments/assets/438b4964-f5db-4005-b992-e8568f6058c1" />
