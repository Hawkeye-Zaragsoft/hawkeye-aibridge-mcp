# Troubleshooting

## `claude` command not found

Claude Code isn't installed or isn't on your PATH. Install from https://docs.claude.com/en/docs/build-with-claude/claude-code and restart your terminal.

## `claude mcp list` doesn't show hawkeye

You may have registered it in a different scope. Re-register with `--scope user`:

```powershell
claude mcp remove hawkeye
claude mcp add hawkeye --scope user -- "C:\Program Files\Hawkeye\AIBridge\HawkeyeAIBridge.exe"
```

## `claude mcp list` shows hawkeye but with 0 tools

The exe was registered but failed to start. Common causes:

- The `AIBridge` folder was moved or deleted after registration.
- Hawkeye itself can't be found — run `hawkeye --version` in a fresh terminal to check.
- Fix: `claude mcp remove hawkeye` then re-register.

## Hawkeye not found

```
Error: Failed to start Hawkeye process
```

1. Open a new terminal and run `hawkeye --version`.
2. If that fails, set `HAWKEYE_PATH` and close/reopen your terminal:
   ```powershell
   [Environment]::SetEnvironmentVariable("HAWKEYE_PATH", "C:\Program Files\Hawkeye\hawkeye.exe", "User")
   ```
3. Environment variables only apply to terminals opened *after* you set them.

## Skill isn't being used by Claude

- Confirm the file exists at `%USERPROFILE%\.claude\skills\hawkeye-search\SKILL.md` **and** that it's a plain text file, not the `.skill` archive under a different name. Right-click it → Properties; if the size matches the original `.skill` file (~14 KB) and it won't open in a text editor, it was renamed instead of extracted — delete it and re-run the `Expand-Archive` step from [install-claude.md](install-claude.md).
- Restart your Claude Code session — Skills are loaded at session start.

## Cursor: connection failed with path error

If Cursor logs show `'C:\Program' is not recognized as an internal or external command`, the path with spaces is being passed unquoted. Use the `cmd /c` workaround:

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

Cursor passes the command path to the shell without quoting it, which breaks paths containing spaces. Wrapping with `cmd /c` works around this.

## VS Code cannot find the MCP server

Check that the command path points to the correct location:

```json
"command": "C:\\Program Files\\Hawkeye\\AIBridge\\HawkeyeAIBridge.exe"
```

If Hawkeye AI Bridge is installed elsewhere, update the path accordingly.

## Hawkeye tools do not appear in VS Code Agent Chat

1. Restart VS Code.
2. Confirm the MCP server configuration is valid JSON.
3. Confirm Hawkeye AI Bridge starts correctly from the command line.
4. Confirm VS Code has MCP/Agent Mode support enabled.

## No results are returned

Check that:

- Hawkeye is installed and has indexed the target project.
- The searched files are included in the Hawkeye index.
- The project path is accessible.
- Hawkeye AI Bridge can communicate with Hawkeye.

## No groups returned

```
No groups available / Empty group list
```

1. Run `hawkeye --getgroups` manually to test.
2. Verify Hawkeye configuration is correct.
3. Check working directory permissions.

## Timeout errors

```
Error: Operation timed out waiting for Hawkeye
```

1. Check if the Hawkeye process is hanging.
2. Check system resources.
3. Restart Hawkeye and try again.

## AI assistant gives poor search instructions

Be explicit in your prompt. Instead of:

```
Find this.
```

Use:

```
Use Hawkeye to search the full project for references to InventoryManager and show the most relevant files before editing anything.
```
