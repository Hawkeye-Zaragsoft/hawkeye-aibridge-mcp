# Troubleshooting

## VS Code cannot find the MCP server

Check that the command path points to the installed Hawkeye AI Bridge executable.

For example:

```json
"command": "C:\\Program Files\\Hawkeye\\HawkeyeAIBridge.exe"
```

If Hawkeye AI Bridge is installed elsewhere, update the path.

## Hawkeye tools do not appear in Agent Chat

Try the following:

1. Restart VS Code.
2. Confirm the MCP server configuration is valid JSON.
3. Confirm that Hawkeye AI Bridge starts correctly from the command line.
4. Confirm that VS Code has MCP/Agent Mode support enabled.

## No results are returned

Check that:

- Hawkeye is installed.
- Hawkeye has indexed the target project.
- The searched files are included in the Hawkeye index.
- The project path is accessible.
- Hawkeye AI Bridge is able to communicate with Hawkeye.

## Paths with spaces fail

Use a full JSON string path. Example:

```json
"command": "C:\\Program Files\\Hawkeye\\HawkeyeAIBridge.exe"
```

Do not manually add extra quote characters inside the JSON value unless the client specifically requires it.

## The MCP server starts but exits immediately

Possible causes:

- Missing Hawkeye installation.
- Invalid command path.
- Missing required runtime dependency.
- License or activation issue.
- The bridge is not configured to run in MCP stdio mode.

## AI assistant gives poor search instructions

Be explicit in your prompt.

Instead of:

```text
Find this.
```

Use:

```text
Use Hawkeye to search the full project for references to InventoryManager and show the most relevant files before editing anything.
```
