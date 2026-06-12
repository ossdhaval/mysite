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

<img width="829" height="744" alt="image" src="https://github.com/user-attachments/assets/9ffdf14f-7ff5-4524-856d-f0dc3f60dc78" />


1. At startup, agent requests tools. Request goes to langchain adapter which talk to MCP client following MCP protocol.
2. MCP client responds with MCP tool objects which the adapter converts into langchain standard `BaseTool` objects and gives it to langgraph agent.
3. When agent receives the prompt string, the LangGraph packages your prompt into a standard langchain `HumanMessage` object. LangGraph binds `BaseTool` objects and `HumanMessage` object to the langchain framework.
4. langchain framework converts these objects into JSON schema as required by the LLM configured. This gives the developer flexibility to replace one LLM with another without any code change because langchain converts suitably.
 ```
  {
  "model": "claude-3-5-sonnet",
  "messages": [{ "role": "user", "content": "Look at my context7 files..." }],
  "tools": [
    {
      "name": "context7__read_repository_structure",
      "description": "Scans the project repository directory layout.",
      "input_schema": {
        "type": "object",
        "properties": {
          "path": { "type": "string", "description": "The root path to scan" }
        },
        "required": ["path"]
      }
    }
  ]
}
```
5. LLM analyses the prompt, and checks its own knowledge and the list of available tools. If it needs to, it'll request to call a tool. This response again is different from each LLM.
```
{
  "content": [],
  "tool_calls": [
    {
      "name": "context7__read_repository_structure",
      "args": { "path": "./src" },
      "id": "call_llm_99"
    }
  ]
}
```
6. This response is converted by the langchain framework into a langchain standard tool call and given to langgraph agent.
7. The agent initiates the tool call via langchain MCP adapter. Adapter converts the langchain specific tool object into a python arguments and gives them to MCP client.
```
# Raw Python data passed downward
tool_name = "read_repository_structure"
arguments = {"path": "./src"}
```
9. MCP client takes these args and turns them into JSON RPC call and sends it over to STDIO or HTTP according to the local or remote server configuration.
```
{
  "jsonrpc": "2.0",
  "method": "tools/call",
  "params": {
    "name": "read_repository_structure",
    "arguments": { "path": "./src" }
  },
  "id": "mcp-req-101"
}
```
10. Remote server processes the request and responds using JSON RPC. 
```
{
  "jsonrpc": "2.0",
  "result": {
    "content": [
      {
        "type": "text",
        "text": "Found build files: pom.xml (Spring Boot Starter dependencies detected)"
      }
    ]
  },
  "id": "mcp-req-101"
}
```
11. The MCP client takes this JSON RPC response and converts it into Python object and gives it to adapter
```
ToolMessage(
    content="Found build files: pom.xml (Spring Boot Starter dependencies detected)",
    tool_call_id="call_llm_99"
)
```
12. Adapter takes the object and converts into langchain objects and gives to the langgraph agent.
13. agent sends the tool response back to the LLM (via langchain framework)
14. LLM takes the tool response and creates a response for the original prompt and send it back to the agent(via  langchain framework)
15. Agent sends the response back to the user
