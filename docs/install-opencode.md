# Install Hawkeye AI Bridge in OpenCode

## Prerequisites

- Hawkeye installed — get it from https://www.zaragsoft.se/downloads
- Hawkeye AI Bridge installed — get it from https://www.zaragsoft.se/aibridge
- A local project indexed by Hawkeye

## Register the MCP server

Add the following to your `opencode.json` (create it in your project root or home directory if it doesn't exist):

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "hawkeye": {
      "type": "local",
      "command": ["C:\\Program Files\\Hawkeye\\AIBridge\\HawkeyeAIBridge.exe"]
    }
  }
}
```

Three things differ from the Claude Code config:

- The key is `"mcp"`, not `"mcpServers"`
- `command` is an **array** of strings, not a `command` + `args` split
- `"type": "local"` is required

## Install the Skill

The Skill is required for OpenCode. Without it, OpenCode will try to call `hawkeye.exe` directly on the command line rather than routing tool calls through the MCP server.

OpenCode expects skills to be extracted from the `.skill` zip archive:

```powershell
$skillDir = "$env:USERPROFILE\.opencode\skills"
New-Item -ItemType Directory -Force -Path $skillDir | Out-Null

$tempZip = "$env:TEMP\hawkeye-search.zip"
Copy-Item "C:\Program Files\Hawkeye\AIBridge\hawkeye-search.skill" $tempZip -Force
Expand-Archive -Path $tempZip -DestinationPath $skillDir -Force
Remove-Item $tempZip
```

## Verify

Restart OpenCode and try: *"Find where PlayerController is defined."*

You should see it call `hawkeye_search_minimal`.

## Troubleshooting

See [troubleshooting.md](troubleshooting.md)
