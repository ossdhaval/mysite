# Model Context Protocol

## Reference:

- Good quick video for creating local agent with MCP (OllamaIndex, Ollama): https://www.youtube.com/watch?v=C64rVY1eN8k


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


## Security

- MCP authorization spec: https://modelcontextprotocol.io/specification/draft/basic/authorization
- MCP clients must add `resource`: The specification now requires client developers to implement RFC 8707 - Resource Indicators for OAuth 2.0. [link](https://den.dev/blog/mcp-authorization-resource/)

### imp

- `resource` and `aud`:

  When an MCP client requests a token, they include a resource parameter (per RFC 8707) specifying the exact MCP server they're accessing. The authorization server then issues a token containing the agent's requested scopes AND an audience claim that binds the token to that specific resource server. If a token is later compromised, it's useless against other MCP servers because the audience claim doesn't match—this severely limits lateral movement.

- This approach also supports resource indicators, which provide even finer resource-level scoping. Instead of just validating that an agent has the documents:write scope, the server can validate that the token's resource indicator matches the specific document being modified, preventing an agent with broad write permissions from modifying resources outside their intended scope.

- Tool groups

- General attribute based access control:

  - Subject attributes (the requester): user role, department, team, security clearance level, or account status
  - Resource attributes (what's being accessed): data classification, ownership, environment (production vs. staging), or sensitivity level
  - Action attributes (what's being done): the specific operation, parameter values, or transaction amounts
  - Environmental attributes (context): time of day, geographic location, IP address, device trust level, or network type
 
- PDP
- Default-Deny Posture and Explicit Allowlisting
- mTLS
- Support OAuth 2.0 Protected Resource Metadata (RFC 8414 and RFC 9728) for authorization server discovery.


Hosts:


#### Permit

Leveraging FastMCP’s Middleware, the Permit.io middleware intercepts all MCP requests to your server and automatically maps MCP methods to authorization checks against your Permit.io policies; covering both server methods and tool execution.

### Communication

- All MCP communication uses JSON-RPC 2.0, a lightweight remote procedure call protocol built on JSON.

  - JSON-RPC messages are UTF-8 encoded and fall into three categories:​

    - Requests contain a jsonrpc field set to "2.0", a unique id for correlation, a method name specifying the operation, and optional params for arguments.
    - Responses return results or errors with the same id to allow the client to correlate the response with its request.
    - Notifications are one-way messages that don't require responses, used for state changes, status updates, or asynchronous events.


- Transport Mechanisms

  MCP supports two primary transport methods for carrying JSON-RPC messages between clients and servers.

  - STDIO Transport (Local)

    STDIO (Standard Input/Output) is used for local server-client communication where the server runs as a subprocess on the same machine as the client.​ The client launches the MCP server as a child process.

    Communication occurs through the server's standard input and output streams:

      - Client writes JSON-RPC messages to the server's stdin
      - Server reads messages from stdin and writes responses to stdout
      - Messages are delimited by newline characters

    - STDIO offers several advantages for local deployments:​

      - Lowest latency: No network stack overhead, achieving 10,000+ operations per second​
      - High security: No network exposure, inherently contained to the local machine
      - Simplicity: No network configuration required
      - One-to-one relationship: A single client-server pair per STDIO connection

    - STDIO is ideal for local CLI tools, IDE extensions, and security-sensitive operations where network exposure should be avoided.

  - Streamable HTTP Transport (Remote)

      Streamable HTTP is the modern standard for remote MCP server communication, replacing the deprecated HTTP+SSE transport. It operates over HTTP/HTTPS and enables cloud deployments and multi-client scenarios.​

    - In Streamable HTTP:

      - Every JSON-RPC message from client to server is sent as an HTTP POST request to the MCP endpoint​
      - The client includes the message in the POST body with appropriate headers
      - The server can respond with either:​

        - A single JSON response (Content-Type: application/json) for simple operations
        - An SSE stream (Content-Type: text/event-stream) for long-running operations or multiple messages
        - Server-to-client messages arrive through SSE streams or HTTP GET requests

    - Streamable HTTP enables:​

      - Remote access: Web and cloud-based MCP servers
      - Multi-client support: Multiple clients connecting to a single server
      - Flexibility: Simple operations return JSON; complex operations use streaming
      - Scalability: Horizontal scaling across multiple server instances

HTTP adds network latency (typically 10-50ms) compared to STDIO but enables distributed architectures.​

