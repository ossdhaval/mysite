# Claude training notes

## Claude Code 101

- Claude code is an agent itself. It has an agentic loop (gather context, take action, verify result). That is what makes it different from a ai chat window. Claude code can:
  - work with files
  - calls tools
  - call LLMs
  - access your terminal and check outputs

### shortcuts

- `shift+tab` to shift between different modes. 


# youtube video notes

## 1

from: https://www.youtube.com/watch?v=9oJySubZRSA

- projects: grouping of related chats. So that claude has the context across all chats. You can set instructions that all chats share. You can upload files to the project. These files are shared across chats within the same project. So, project is claude's memory about a topic.
- memory: memory is what claude knows about you as a person. Settings -> memory. You can edit memory by chatting with claude. Claude derives these memories from chats.
- connectors: allows you to connect claude with different apps like gmail. If you don't find a connector for app that you need, see if that app has an MCP server. If it is, then you can add a custom connector which simply asks for mcp server url.
- Skills: skills are text markdown files. They are used to teach claude how to do a particular task step-by-step.
- cowork: This is where claude works autonomously. You can allow it access to only certain folders on your desktop. Everything else stays off limit. It can read and write files from those folders. 
- schedule: you can ask claude to perform tasks at set time and date (may be repeatedly). you give a prompt about a task (summarize all my emails). Set frequency (every morning) etc.

- Claude design: for web page designs
- b
