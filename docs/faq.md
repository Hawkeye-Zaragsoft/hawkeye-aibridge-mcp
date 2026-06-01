# FAQ

## Is Hawkeye AI Bridge open source?

No. Hawkeye and Hawkeye AI Bridge are proprietary software owned by Zaragsoft.

This repository contains public documentation, configuration examples, and MCP metadata only.

## Can people change the official Hawkeye AI Bridge?

No. Users can suggest documentation changes in this repository, but they cannot change the proprietary Hawkeye AI Bridge implementation.

## Does Hawkeye upload my code?

No. Hawkeye runs locally/on-premises. Your code is never uploaded.

## Does Hawkeye use AI?

Hawkeye itself does not use AI for indexing or searching.

Hawkeye AI Bridge allows MCP-compatible AI assistants to query Hawkeye, but Hawkeye's own search remains entirely local.

## Which AI clients does this work with?

Hawkeye AI Bridge works with any MCP-compatible client. Verified clients include:

- **Claude Desktop** — install via `.mcpb` bundle, no manual config needed.
- **Claude Code (CLI)** — register the exe with `claude mcp add`, install the Skill.
- **VS Code / GitHub Copilot** — register the exe in `.vscode/mcp.json` or user `mcp.json`, use Agent mode.
- **Cursor** — register via Settings → Tools & MCP, use the `cmd /c` workaround for paths with spaces.
- **OpenCode** — add to `opencode.json`, extract the `.skill` zip for the skill.

## Do I need Hawkeye installed?

Yes. Hawkeye AI Bridge requires Hawkeye to be available locally. You can download a trial version at https://www.zaragsoft.se/downloads

## Do I need to install the Skill?

For **Claude Code**, **Claude Desktop**, **Cursor**, and **OpenCode** — yes, the Skill teaches the AI when and how to use Hawkeye tools correctly.

For **VS Code / GitHub Copilot** — no, VS Code uses Copilot's own context system and doesn't use `.skill` files.
