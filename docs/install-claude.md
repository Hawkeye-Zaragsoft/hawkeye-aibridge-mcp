# Install Hawkeye AI Bridge for Claude

---

## Claude Desktop

**You don't need a manual config for Claude Desktop.** Download `Hawkeye.mcpb` from the release page and install it directly:

- If `.mcpb` is a recognised file type on your system: double-click the file.
- Otherwise: go to **Settings → Extensions → Install Extension** and select the file.

---

## Claude Code (CLI)

### Quick Start (5 steps)

1. **Install Hawkeye** from https://www.zaragsoft.se/downloads if you haven't already.
2. **Move the `AIBridge` folder** to a permanent location — recommended: `C:\Program Files\Hawkeye\AIBridge\`. Don't run it from Downloads; the registered path must keep working.
3. **Register the MCP server** with Claude Code:
   ```powershell
   claude mcp add hawkeye --scope user -- "C:\Program Files\Hawkeye\AIBridge\HawkeyeAIBridge.exe"
   ```
4. **Install the Skill** so Claude knows when to use Hawkeye. `hawkeye-search.skill` is a zip archive (it just contains `SKILL.md`), so it needs to be extracted, not renamed:
   ```powershell
   $skillDir = "$env:USERPROFILE\.claude\skills\hawkeye-search"
   New-Item -ItemType Directory -Force -Path $skillDir | Out-Null
   Expand-Archive -Path "C:\Program Files\Hawkeye\AIBridge\hawkeye-search.skill" -DestinationPath $skillDir -Force
   ```
5. **Verify** — close and reopen your terminal, then run:
   ```powershell
   claude mcp list
   ```
   You should see `hawkeye` with 9 tools available.

### Make sure Claude Code can find Hawkeye

**Option A (recommended): Set `HAWKEYE_PATH`**

```powershell
[Environment]::SetEnvironmentVariable("HAWKEYE_PATH", "C:\Program Files\Hawkeye\hawkeye.exe", "User")
```

> Close and reopen your terminal after setting an environment variable.

**Option B: Add Hawkeye to PATH via Windows GUI**

1. Press `Win`, type **Environment Variables**, open **Edit the system environment variables**.
2. Click **Environment Variables…** → under **User variables**, select **Path** → **Edit…** → **New**.
3. Add `C:\Program Files\Hawkeye` and click OK on all dialogs.
4. Restart your terminal.

### Notes

- **`--scope user`** makes Hawkeye available in every Claude Code session, not just the current folder.
- **The `--` separator is required.** It tells Claude Code where its own flags end and the registered command begins.

### Example prompts

- Use Hawkeye to find all references to this class.
- Search the workspace for where this asset name is used.
- Find likely files related to the inventory system in group 4,7.
- List groups inside Hawkeye to find all the groups.
