# Hawkeye AI Bridge MCP Server

Use Hawkeye from VS Code Agent Chat and other MCP-compatible AI coding assistants.

Hawkeye AI Bridge exposes Hawkeye’s fast local search capabilities and overview through the Model Context Protocol (MCP), making it possible for AI coding assistants to search large codebases, assets, sounds files, models, text files, localization files, and project content through Hawkeye.

Hawkeye runs locally/on-premises. Your code is not uploaded by Hawkeye, and Hawkeye itself does not use AI for indexing or searching.

This repository contains setup instructions, configuration examples, and MCP metadata only. Hawkeye and Hawkeye AI Bridge are proprietary software owned by Zaragsoft.

## What is this?

This repository is the official public setup and discovery repository for using Hawkeye AI Bridge as an MCP server.

It does not contain the proprietary Hawkeye AI Bridge source code.

## Why use Hawkeye AI Bridge with VS Code?

Hawkeye helps developers quickly search and understand large projects. With MCP support, VS Code Agent Chat and other MCP-compatible tools can ask Hawkeye for fast local search results saving tokens on each call using it.

Typical use cases:

- Find all references to a class, function, symbol, asset, localization key, or file.
- Search large codebases without relying only on editor search.
- Help AI coding assistants understand more of the project before making changes.
- Navigate large game/software projects with less reliance on tribal knowledge.
- Keep search local/on-premises.
- Better overview.

## Installation

1. Download and install Hawkeye from:
  https://www.zaragsoft.se/downloads

2. Download and install Hawkeye AI Bridge from:
  https://www.zaragsoft.se/aibridge

3. Open VS Code.

4. Add the MCP server configuration.

5. Open Copilot Chat in Agent Mode.

6. Use the Hawkeye MCP tools from Agent Chat.

## VS Code MCP configuration

### Windows example

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

Adjust the path if Hawkeye AI Bridge is installed somewhere else.

## Example prompts

Ask your AI coding assistant:

- Use Hawkeye to find all references to this class.
- Search the workspace for where this asset name is used.
- Find likely files related to the inventory system.
- Search for this localization key across the project.
- Find where this Blueprint or Unreal asset is referenced.
- Show me files related to feature loadout before editing code.
- Use Hawkeye to find code and content references before changing this file.

## Privacy and security

- Hawkeye runs locally/on-premises.
- Hawkeye does not upload your source code.
- Hawkeye itself does not use AI for indexing or searching.
- The MCP server only exposes Hawkeye functionality to tools you configure locally.
- You control which MCP clients can connect to it.
- Always review AI-generated code changes before applying them.

## Requirements

- Hawkeye installed.
- Hawkeye AI Bridge installed.
- VS Code with Agent Mode / MCP support.
- A local project indexed by Hawkeye. Video on how to setup here.
https://www.youtube.com/watch?v=l1J-G36QSwI

## Supported platforms

- Windows: supported.

## Repository contents

```text
hawkeye-aibridge-mcp/
  README.md
  LICENSE.md
  SECURITY.md
  CHANGELOG.md

  .mcp/
    server.json

  examples/
    vscode-mcp-windows.json
    vscode-mcp-linux.json
    claude-desktop-example.json

  docs/
    install-vscode.md
    install-claude.md
    troubleshooting.md
    tools.md
    privacy-and-security.md
    faq.md

  images/
    .gitkeep
```

## Links

- Hawkeye AI Bridge: https://www.zaragsoft.se/aibridge
- Hawkeye: https://www.zaragsoft.se/
- Support: info@zaragsoft.se

## Ownership

Hawkeye and Hawkeye AI Bridge are proprietary software owned by Zaragsoft.

This repository only contains public documentation, configuration examples, and MCP metadata for installation and discovery.
