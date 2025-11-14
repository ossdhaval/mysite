# Model Context Protocol

## Notes from [mcp for beginners hands-on repo](https://github.com/microsoft/mcp-for-beginners/tree/main)

- very good to get high-level picture of what MCP is and overall usefulness: https://github.com/microsoft/mcp-for-beginners/blob/main/00-Introduction/README.md
- [List of MCP servers](https://github.com/modelcontextprotocol/servers?tab=readme-ov-file#-third-party-servers)

### High level flow:

MCP servers operate in the following way:

- Request Flow:
  - A request is initiated by an end user or software acting on their behalf.
  - The MCP Client sends the request to an MCP Host, which manages the AI Model runtime.
  - The AI Model receives the user prompt and may request access to external tools or data via one or more tool calls.
  - The MCP Host, not the model directly, communicates with the appropriate MCP Server(s) using the standardized protocol.
- MCP Host Functionality:
  - Tool Registry: Maintains a catalog of available tools and their capabilities.
  - Authentication: Verifies permissions for tool access.
  - Request Handler: Processes incoming tool requests from the model.
  - Response Formatter: Structures tool outputs in a format the model can understand.
- MCP Server Execution:
  - The MCP Host routes tool calls to one or more MCP Servers, each exposing specialized functions (e.g., search, calculations, database queries).
  - The MCP Servers perform their respective operations and return results to the MCP Host in a consistent format.
  - The MCP Host formats and relays these results to the AI Model.
- Response Completion:
  - The AI Model incorporates the tool outputs into a final response.
  - The MCP Host sends this response back to the MCP Client, which delivers it to the end user or calling software.

### Architecture

[Reference](https://github.com/microsoft/mcp-for-beginners/blob/main/01-CoreConcepts/README.md#mcp-architecture-a-deeper-look)

- MCP Hosts: Programs like VSCode, Claude Desktop, IDEs, or AI tools that want to access data through MCP
- MCP Clients: Protocol clients that maintain 1:1 connections with servers
- MCP Servers: Lightweight programs that each expose specific capabilities through the standardized Model Context Protocol
- Local Data Sources: Your computer's files, databases, and services that MCP servers can securely access
- Remote Services: External systems available over the internet that MCP servers can connect to through APIs.

Hosts:

