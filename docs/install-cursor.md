# Install Hawkeye AI Bridge in Cursor

## Prerequisites

- Hawkeye installed — get it from https://www.zaragsoft.se/downloads
- Hawkeye AI Bridge installed — get it from https://www.zaragsoft.se/aibridge
- A local project indexed by Hawkeye

## Register the MCP server

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

> **Why `cmd /c`?** Cursor passes the command path to the shell without quoting it, which breaks paths containing spaces (like `C:\Program Files\`). Wrapping it with `cmd /c` works around this.

Adjust the path if Hawkeye AI Bridge is installed somewhere else.

## Install the Skill

The Skill teaches Cursor when and how to use the Hawkeye tools. Without it, the agent may try to call `hawkeye.exe` directly from the shell instead of routing calls through the MCP server.

```powershell
$skillDir = "$env:USERPROFILE\.cursor\skills\hawkeye-search"
New-Item -ItemType Directory -Force -Path $skillDir | Out-Null

$tempZip = "$env:TEMP\hawkeye-search.zip"
Copy-Item "C:\Program Files\Hawkeye\AIBridge\hawkeye-search.skill" $tempZip -Force
Expand-Archive -Path $tempZip -DestinationPath "$env:TEMP\hawkeye-search-extract" -Force
Copy-Item "$env:TEMP\hawkeye-search-extract\hawkeye-search\SKILL.md" "$skillDir\SKILL.md" -Force
```

## Verify

Restart Cursor, then start a new agent chat and try:

- *"List Hawkeye groups"* — should call `hawkeye_get_groups`
- *"Find PlayerController in group 12"* — should call `hawkeye_search_minimal`

## Troubleshooting

If Cursor logs show `'C:\Program' is not recognized as an internal or external command`, the path with spaces is being passed unquoted. Make sure you are using the `cmd /c` config shown above — not a direct path as the command value.

See also: [troubleshooting.md](troubleshooting.md)
