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

## why fastmcp is called a framework and not just a library that implements MCP protocol

- In a simple library, you call its functions when you need them. In FastMCP, the framework calls your code. You use built-in Python decorators like @mcp.tool(), @mcp.resource(), and @mcp.prompt() to register your functions. 

- Once decorated, FastMCP takes control of the execution lifecycle, managing how and when those functions are exposed and executed by a Large Language Model (LLM).

- FastMCP doesn't just provide a singular utility; it provides a comprehensive toolkit to take an application from prototype to production

 - Built-in test clients for local debugging
 - Native enterprise authentication modules (Google, GitHub, Azure)
 - Mechanisms to render interactive user interfaces (UIs) directly inside LLM chat conversations

## MCP host 

- creates and manages clients
- aggregates tools, prompts etc across available clients
- agents talk to hosts. When agent/llm calls a tool, the host will

## How using fastMCP easier than building MCP server using MCP protocol directly

FastMCP simplifies MCP server creation significantly:

- Traditional MCP Server:
  - Define tool schemas manually with JSON
  - Implement list_tools(), call_tool() handlers
  - Handle resource URIs and content types
  - Set up STDIO transport manually
- FastMCP Server:
  - Use @mcp.tool() decorator - schema generated automatically
  - Use @mcp.resource() decorator with URI templates
  - Use @mcp.prompt() decorator for templates
  - Call mcp.run() - transport handled automatically

FastMCP uses Python type hints to generate tool schemas, making your code cleaner and reducing boilerplate.

## Notes about authorization for MCP server for jans-config-api 


- tools can be exposed based on authorization
- prompts can be exposed based on authorization
- mcp protocol has a context object which has the details about underlying MCP session
  - the Context object:  The Context object provides a clean interface to access MCP features within your functions, including:
       - Logging: Send debug, info, warning, and error messages back to the client
       - Progress Reporting: Update the client on the progress of long-running operations
       - Resource Access: List and read data from resources registered with the server
       - Prompt Access: List and retrieve prompts registered with the server
       - LLM Sampling: Request the client’s LLM to generate text based on provided messages
       - User Elicitation: Request structured input from users during tool execution
       - Session State: Store data that persists across requests within an MCP session
       - Session Visibility: Control which components are visible to the current session
       - Request Information: Access metadata about the current request
       - Server Access: When needed, access the underlying FastMCP server instance
- MCP server can use LLM sampling to Request the client’s LLM to generate text based on provided messages
- See the [permissions](#permissions). Here, cedarling can play a role in defining policies that allow, deny, ask
- See the [elicitation](#elicitation). here cedarling can play a role in applying a policy to an event based on the context and trigger appropriate elicitation
- so in MCP when an LLM asks something (tool call, resource etc), the request goes through two gates: permissions(clientside), elicitation(server side).
- Policies should be like below:
 - <img width="1839" height="872" alt="image" src="https://github.com/user-attachments/assets/d568649b-20a7-4c36-a0dd-fe6cf67ac837" />



## client-server flow

### client connection flow

```
1. Launch client with server script path
   ↓
2. Create StdioServerParameters
   ↓
3. Launch server as subprocess via stdio_client
   ↓
4. Create ClientSession with read/write streams
   ↓
5. Call session.initialize() (MCP handshake)
   ↓
6. Ready for operations
```

### Resource reading flow

```
User: types "read"
   ↓
User: enters "file://resources/README.md"
   ↓
Client: calls session.read_resource(uri)
   ↓
[JSON-RPC request sent via stdin]
   ↓
Server: receives request with URI "file://resources/README.md"
   ↓
Server: matches URI to template pattern "file://resources/{filename}"
   ↓
Server: extracts parameter: filename = "README.md"
   ↓
Server: calls read_resource_file("README.md")
   ↓
Server: function reads file and returns content
   ↓
[JSON-RPC response sent via stdout]
   ↓
Client: receives result object
   ↓
Client: displays result.contents[0].text
```

## stdio vs streamable HTTP

- streamable HTTP superseeds SSE
- in stdio, client itself create a server instance. So, one client, one server. While in streamable HTTP, server is independent and multiple clients can connect to same server.

## Sampling

Here MCP server sends a request to client to invoke LLM capabilities and return the response generated by LLM. Before sending the request to LLM, the client asks for permission from the user. 

Also, for this to happen, client should have advertised that it provides sampling. This should happen at the initilization phase as part of capability advertisement. Server should know how to work when client doesn't support sampling.

Here is an example of sampling request from server to a client:

<img width="907" height="410" alt="image" src="https://github.com/user-attachments/assets/ec26fc99-3032-4f33-8855-27849e64e9ae" />


## permissions

- On the client side
 - In the MCP protocol, `permissions` work on the client side and not on the server side.
 - permissions are stored in the `permissions.json`
 - policies are of 3 types. Allow, deny and ask.
 - If policy is deny or ask, then the server doesn't even come into the picture
 - if ask, then if the user allows, then only the mcp client sends request to the server

## elicitation

- elicitation starts from server
- server sends a json structured elicitation request to the client
- elicitation usecases: multi-step workflows, destructive operations that require confirmations+reason, missing parameters in earlier requests, compliance documentaion requiring justification, security acknowledgements and risk awareness
 - <img width="1861" height="952" alt="image" src="https://github.com/user-attachments/assets/1bb9c9b8-6c52-4c87-b366-aa344cf188c2" />
- Server can classify different requests (tool calls, resource access etc) in following categories. And based on categories, it can send different kinds of elicitation requests
- audit logging is critical. So, client does logging of every policy decision. May be server should do the same as well.
 - <img width="1848" height="949" alt="image" src="https://github.com/user-attachments/assets/f341708f-001f-458d-a208-dafc0e0f5e35" />

