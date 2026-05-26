# Install Hawkeye AI Bridge in VS Code

This guide explains how to connect Hawkeye AI Bridge to VS Code Agent Chat through MCP.

## Prerequisites

- Hawkeye installed.
- Hawkeye AI Bridge installed.
- VS Code with Agent Mode / MCP support.
- A local project indexed by Hawkeye.

## Windows configuration

Add this MCP server configuration to VS Code:

```json
{
  "servers": {
    "hawkeye": {
      "type": "stdio",
      "command": "C:\\Program Files\\Hawkeye\\HawkeyeAIBridge.exe",
      "args": []
    }
  }
}
```

Adjust the executable path if Hawkeye AI Bridge is installed elsewhere.

## Verify installation

After adding the configuration:

1. Restart VS Code if needed.
2. Open Copilot Chat.
3. Switch to Agent Mode.
4. Check that Hawkeye tools are available.
5. Try asking a search question related to your project.

## Example prompts

- Use Hawkeye to find references to this symbol.
- Search the project for this asset name.
- Find files related to the login system.
- Use Hawkeye before editing this file and show related files.
- Hawkeye get group - Should list the groups that you have setup inside Hawkeye.
