# Hawkeye AI Bridge MCP Server

Use Hawkeye from AI coding assistants via the Model Context Protocol (MCP).

Hawkeye AI Bridge exposes Hawkeye's fast local search capabilities through MCP, making it possible for AI coding assistants to search large codebases, assets, sound files, models, text files, localization files, and project content through Hawkeye.

Hawkeye runs locally/on-premises. Your code is not uploaded by Hawkeye, and Hawkeye itself does not use AI for indexing or searching.

<img width="1371" height="841" alt="image" src="https://github.com/user-attachments/assets/2ce83c09-1302-4e07-b226-d23d14b676ee" />

---

## Table of Contents

- [What is this?](#what-is-this)
- [Why use Hawkeye AI Bridge?](#why-use-hawkeye-ai-bridge)
- [Installation](#installation)
- [Client Setup](#client-setup)
  - [VS Code](#vs-code)
  - [Cursor](#cursor)
  - [Claude Desktop](#claude-desktop)
  - [Claude Skill](#claude-skill)
  - [OpenCode](#opencode)
- [Example Prompts](#example-prompts)
- [Privacy and Security](#privacy-and-security)
- [Requirements](#requirements)
- [Supported Platforms](#supported-platforms)
- [Links](#links)
- [Ownership](#ownership)

---

## What is this?

This repository is the official public setup and discovery repository for using Hawkeye AI Bridge as an MCP server.

It does not contain the proprietary Hawkeye AI Bridge source code.

---

## Why use Hawkeye AI Bridge?

Hawkeye helps developers quickly search and understand large projects reducing tribal knowledge on the way. With MCP support, AI coding assistants can ask Hawkeye for fast local search results, saving lots of tokens on each call.

Typical use cases:

- Find all references to a class, function, symbol, asset, localization key, or file.
- Search large codebases without relying only on editor search.
- Help AI coding assistants understand more of the project before making changes.
- Navigate large game/software projects with less reliance on tribal knowledge.
- Keep search local/on-premises.
- Better overview.
- Token savings listed below.

---

## Installation

1. Download and install Hawkeye from:
   https://www.zaragsoft.se/downloads
   Video walkthrough: https://www.youtube.com/watch?v=l1J-G36QSwI

2. Download and install Hawkeye AI Bridge from:
   https://www.zaragsoft.se/aibridge

3. Follow the setup guide for your AI client below.

---

## Client Setup

### VS Code

Open your MCP settings and add:

```json
{
  "servers": {
    "hawkeye": {
      "type": "stdio",
      "command": "C:\\Program Files\\Hawkeye\\AIBridge\\HawkeyeAIBridge.exe",
      "args": []
    }
  }
}
```

Then open Copilot Chat in Agent Mode and use the Hawkeye tools.

Adjust the path if Hawkeye AI Bridge is installed somewhere else.

---

### Cursor

Open **Settings → Tools & MCP → New MCP Server** and add:

```json
{
  "mcpServers": {
    "hawkeye": {
      "command": "cmd",
      "args": ["/c", "C:\\Program Files\\Hawkeye\\AIBridge\\HawkeyeAIBridge.exe"],
      "env": {}
    }
  }
}
```

Adjust the path if Hawkeye AI Bridge is installed somewhere else.

---

### Claude Desktop

Add the following to your Claude Desktop MCP configuration:

```json
{
  "mcpServers": {
    "hawkeye": {
      "type": "stdio",
      "command": "C:\\Program Files\\Hawkeye\\AIBridge\\HawkeyeAIBridge.exe",
      "args": []
    }
  }
}
```

See `examples/claude-desktop-example.json` for a full example.

---

### Claude Skill

Copy `hawkeye-search.skill` to one of these locations:

**Global (all projects):**
```
~/.claude/skills/
```

**Workspace-specific:**
```
.claude/skills/
```

---

### OpenCode

Add to your OpenCode MCP configuration:

```json
{
  "mcpServers": {
    "hawkeye": {
      "type": "stdio",
      "command": "C:\\Program Files\\Hawkeye\\AIBridge\\HawkeyeAIBridge.exe",
      "args": []
    }
  }
}
```

Adjust the path if Hawkeye AI Bridge is installed somewhere else.

---

## Example Prompts

Ask your AI coding assistant:

- List groups inside Hawkeye to find all the groups.
- Use Hawkeye to find all references to this class.
- Search the workspace for where this asset name is used.
- Find likely files related to the inventory system in group 4,7.
- Search for this localization key across the project.
- Find where this Blueprint or Unreal asset is referenced.
- Show me files related to feature loadout before editing code.
- Find all the sounds for explosion inside groups 1,5,7
- Use Hawkeye to find code and content references before changing this file.
- If you do not specify any groups then all groups will be used.

---

## Privacy and Security

- Hawkeye runs locally/on-premises.
- Hawkeye does not upload your source code.
- Hawkeye itself does not use AI for indexing or searching.
- The MCP server only exposes Hawkeye functionality to tools you configure locally.
- You control which MCP clients can connect to it.
- Always review AI-generated code changes before applying them.
- Our privacy guidelines are available here - https://www.zaragsoft.se/privacy

---

## Requirements

- Hawkeye installed.
- Hawkeye AI Bridge installed.
- An MCP-compatible AI coding assistant (VS Code, Cursor, Claude Desktop, etc.).
- A local project indexed by Hawkeye.

---

## Supported Platforms

- Windows: supported.

---

## Links

- Hawkeye AI Bridge: https://www.zaragsoft.se/aibridge
- Hawkeye: https://www.zaragsoft.se/
- Support: info@zaragsoft.se

---

## Ownership

Hawkeye and Hawkeye AI Bridge are proprietary software owned by Zaragsoft.

This repository only contains public documentation, configuration examples, and MCP metadata for installation and discovery.