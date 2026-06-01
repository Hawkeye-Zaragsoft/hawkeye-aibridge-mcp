# Install Hawkeye AI Bridge in VS Code

This guide explains how to connect Hawkeye AI Bridge to VS Code Agent Chat through MCP.

## Prerequisites

- Hawkeye installed — get it from https://www.zaragsoft.se/downloads
- Hawkeye AI Bridge installed — get it from https://www.zaragsoft.se/aibridge
- VS Code with GitHub Copilot and Agent Mode support
- A local project indexed by Hawkeye

## Quick install (default path)

[![Install in VS Code](https://img.shields.io/badge/VS_Code-Add_Hawkeye_MCP-0098FF?style=flat&logo=visualstudiocode)](vscode:mcp/install?%7B%22name%22%3A%22hawkeye%22%2C%22command%22%3A%22C%3A%5C%5CProgram%20Files%5C%5CHawkeye%5C%5CAIBridge%5C%5CHawkeyeAIBridge.exe%22%7D)

Click the button above, then click **Allow** in VS Code.

## Manual setup

Add this to your `.vscode/mcp.json` (create the file if it doesn't exist):

```json
{
  "servers": {
    "hawkeye": {
      "type": "stdio",
      "command": "C:\\Program Files\\Hawkeye\\AIBridge\\HawkeyeAIBridge.exe"
    }
  }
}
```

To make Hawkeye available across all projects, add it to your user-level config instead:

```json
// %APPDATA%\Code\User\mcp.json
{
  "servers": {
    "hawkeye": {
      "type": "stdio",
      "command": "C:\\Program Files\\Hawkeye\\AIBridge\\HawkeyeAIBridge.exe"
    }
  }
}
```

Adjust the path if Hawkeye AI Bridge is installed somewhere else.

## Using Hawkeye in Copilot Chat

1. Open Copilot Chat (`Ctrl+Alt+I`)
2. Switch to **Agent mode** (the dropdown at the top — must be Agent, not Ask or Edit)
3. Try: *"Search for findTeam in my codebase"*

> **Note:** The `hawkeye-search.skill` file is for Claude Code and Claude Desktop only — VS Code uses Copilot's own context system and doesn't need it.

## Example prompts

- Use Hawkeye to find references to this symbol.
- Search the project for this asset name.
- Find files related to the login system.
- Use Hawkeye before editing this file and show related files.
- List Hawkeye groups to see what is indexed.
