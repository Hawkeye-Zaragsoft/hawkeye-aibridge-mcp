# Privacy and Security

Hawkeye AI Bridge is designed to expose Hawkeye functionality to MCP-compatible tools running on the user's machine.

## Local-first design

- Hawkeye runs locally/on-premises.
- Hawkeye does not upload your source code.
- Hawkeye itself does not use AI for indexing or searching.
- Search is performed against local Hawkeye indexes.

## MCP client access

The MCP server only exposes functionality to MCP clients that you configure.
MCP server does not work on http. Local only.

Only connect MCP clients that you trust.

## AI assistant behavior

Hawkeye can provide search results to an AI assistant, but users should always review AI-generated code changes before applying them.

## Proprietary software

Hawkeye and Hawkeye AI Bridge are proprietary software owned by Zaragsoft.

This repository does not include proprietary source code.
