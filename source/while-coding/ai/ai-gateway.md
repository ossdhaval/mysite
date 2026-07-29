# AI Gateways

May be there are two types:

- Agent gateway
- MCP gateway

## Agent gateways

Usecases:

https://www.youtube.com/watch?v=A1xIBCE0mcA

- Credentials management
    Give LLM api key to gateway and not to every app and agent
- Rate limiting
- Usage analytics
- Guardrails
    Requests and prompts going to the LLM can be filtered, cleaned and moderated. Responses from LLM can also be monitored and acted upon. 
- Abstraction
    Build LLM provider agnostic apps and agents by using generic APIs exposed by agent gateway.
  

## Gateways

- [Agentgateway](https://agentgateway.dev/) part of Agentic AI foundation
- [Microsoft MCP gateway](https://github.com/microsoft/mcp-gateway)
- [obot](https://obot.ai/)
