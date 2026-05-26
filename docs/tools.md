# Hawkeye AI Bridge — Tool Reference

This document describes all MCP tools exposed by Hawkeye AI Bridge. These tools are available in Claude Desktop, Claude Code (CLI), and VS Code with GitHub Copilot.

---

## Search Tools

### hawkeye_search_minimal

Searches the indexed Hawkeye project and returns results as compact `file:line` pairs. This is the recommended tool for most searches — it uses 85–91% fewer tokens than a full text search while returning the same locations.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `query` | string | ✅ | The search term — symbol name, filename, string literal, asset name, etc. |
| `groupMasks` | string[] | ❌ | Filter results to specific Hawkeye groups (e.g. `["Source", "Content"]`). Omit to search all groups. |
| `maxResults` | integer | ❌ | Maximum number of results to return. Defaults to the value in settings.json (50). |

**Returns:** A JSON object with `query`, `total_results`, and a `results` array of `{ file, line }` pairs.

**Example prompts:**
- *"Search for PlayerController using Hawkeye."*
- *"Find all references to MAX_PLAYER_COUNT."*
- *"Use Hawkeye to locate the InventoryManager class."*
- *"Search for harvesterunderattack in the Source group only."*

**Example output:**
```json
{
  "query": "PlayerController",
  "total_results": 47,
  "results": [
    { "file": "D:/Project/Source/Player/PlayerController.cpp", "line": 1 },
    { "file": "D:/Project/Source/Player/PlayerController.h", "line": 1 },
    { "file": "D:/Project/Source/GameMode/GameMode.cpp", "line": 34 }
  ]
}
```

---

### hawkeye_search

Searches the indexed Hawkeye project and returns full results including file paths, line numbers, and the matching code or content snippet. Use this when you need context around each match, for example when building an interactive artifact or doing a detailed analysis.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `query` | string | ✅ | The search term. |
| `groupMasks` | string[] | ❌ | Filter results to specific Hawkeye groups. Omit to search all groups. |
| `maxResults` | integer | ❌ | Maximum number of results to return. Defaults to the value in settings.json (50). |

**Returns:** Full Hawkeye search response with file paths, line numbers, and content snippets.

**When to use `hawkeye_search` vs `hawkeye_search_minimal`:**
- Use `hawkeye_search_minimal` for quick lookups and navigation — much cheaper on tokens.
- Use `hawkeye_search` when you need to read the matched content, for example to analyse code or build a browseable results artifact.

**Example prompts:**
- *"Use Hawkeye full search to find all player damage code and analyse it."*
- *"Search for OnDeath and show me the surrounding code."*
- *"Find all usages of ThePlayerList and give me context around each one."*

---

## Group Tools

### hawkeye_get_groups

Returns all search groups configured in the user's Hawkeye installation. Groups are named collections of indexed paths — for example `Source`, `Content`, `Plugins`, `Config`. Use this before searching when you want to scope a search to a specific part of the project.

**Parameters:** None.

**Returns:** A list of available group names and their configurations.

**Example prompts:**
- *"What Hawkeye groups are available?"*
- *"Show me the Hawkeye groups so I can decide which one to search."*
- *"List all indexed groups in Hawkeye."*

**Example output:**
```json
{
  "groups": [
    { "name": "Source", "path": "D:/Project/Source" },
    { "name": "Content", "path": "D:/Project/Content" },
    { "name": "Plugins", "path": "D:/Project/Plugins" }
  ]
}
```

---

## Editor Tools

### hawkeye_get_editors

Returns all editors configured in the user's Hawkeye installation. Editors are the applications Hawkeye can open files in — for example VS Code, Visual Studio, Notepad++, or Perforce. Use this before calling `hawkeye_execute_editor` to get the correct editor path and parameter format.

**Parameters:** None.

**Returns:** A list of configured editors with their paths and parameter templates.

**Example prompts:**
- *"What editors does Hawkeye have configured?"*
- *"List the available editors before opening this file."*

**Example output:**
```json
{
  "editors": [
    {
      "name": "VS Code",
      "path": "C:/Program Files/Microsoft VS Code/Code.exe",
      "parameters": "--goto \"%FILE%:%LINE%\""
    },
    {
      "name": "Notepad++",
      "path": "C:/Program Files/Notepad++/notepad++.exe",
      "parameters": "-n%LINE% \"%FILE%\""
    }
  ]
}
```

---

### hawkeye_execute_editor

Opens a specific file at a specific line number in a configured editor. Typically used after a search — the user picks a result and this tool opens it directly in their editor of choice.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `editorPath` | string | ✅ | Full path to the editor executable. |
| `filePath` | string | ✅ | Full path to the file to open. |
| `lineNumber` | integer | ✅ | The line number to jump to inside the file. |
| `parameters` | string | ✅ | The editor's argument template. Use `%FILE%` and `%LINE%` as placeholders — these are substituted automatically. |

**Returns:** `{ success: true, message: "Opened <filename> in editor at line <n>" }`

**Example prompts:**
- *"Open PlayerController.cpp at line 34 in VS Code."*
- *"Open that result in Notepad++."*
- *"Jump to that file in my editor."*

> **Tip:** Call `hawkeye_get_editors` first to get the correct `editorPath` and `parameters` format for the user's configured editors.

---

## System Tools

### hawkeye_health_check

Verifies that Hawkeye is installed, reachable, and responding. Useful for diagnosing connection problems before running searches.

**Parameters:** None.

**Returns:** `{ status: "healthy" | "unhealthy", message: string }`

**Example prompts:**
- *"Check if Hawkeye is running."*
- *"Is Hawkeye accessible?"*
- *"Run a Hawkeye health check."*

**Example output:**
```json
{ "status": "healthy", "message": "Hawkeye is running and accessible" }
```

---

### validate_hawkeye_path

Checks whether the Hawkeye executable path currently saved in settings actually exists on disk. Use this when `hawkeye_health_check` fails or when the user reports Hawkeye is not being found.

**Parameters:** None.

**Returns:** `{ isValid: boolean, path: string, message: "valid" | "invalid" | "error: ..." }`

**Example prompts:**
- *"Check if the Hawkeye path in settings is correct."*
- *"Validate the Hawkeye installation path."*

---

## Settings Tools

### get_settings

Reads the current Hawkeye AI Bridge configuration from `settings.json`. Returns the Hawkeye executable path, the programopener path, the default max results, and the case sensitivity setting.

**Parameters:** None.

**Returns:**

| Field | Type | Description |
|-------|------|-------------|
| `hawkeyePath` | string | Path to `hawkeye.exe` |
| `programopenerPath` | string | Path to `programopener.exe` (derived from `hawkeyePath` if not set explicitly) |
| `maxResults` | integer | Default maximum search results |
| `caseSensitive` | integer | Case sensitivity: `0` = case sensitive, `1` = case insensitive, `2` = smart case |

**Example prompts:**
- *"Show me the current Hawkeye settings."*
- *"What is the Hawkeye path configured in settings?"*

---

### save_settings

Writes updated configuration to `settings.json`. Use this to change the Hawkeye executable path, the default result limit, or case sensitivity behaviour. The `programopenerPath` is derived automatically from `hawkeyePath`.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `hawkeyePath` | string | ❌ | Full path to `hawkeye.exe`. |
| `maxResults` | integer | ❌ | New default maximum results. |
| `caseSensitive` | integer | ❌ | `0` = case sensitive, `1` = case insensitive, `2` = smart case. |

All parameters are optional — omit any you do not want to change.

**Returns:** `{ success: true, message: "Settings saved successfully" }`

**Example prompts:**
- *"Update the Hawkeye path to D:/Tools/Hawkeye/hawkeye.exe."*
- *"Set the default max results to 100."*
- *"Change Hawkeye to case-insensitive search."*

---

## Notes

- **Token efficiency:** Use `hawkeye_search_minimal` by default. Switch to `hawkeye_search` only when you need content snippets. The difference is 85–91% fewer tokens for the same result set.
- **Group filtering:** Pass `groupMasks` to limit searches to specific indexed groups. Searching fewer groups is faster and returns more focused results.
- **Tool availability:** The tools available may vary slightly depending on the installed version of Hawkeye AI Bridge. Call `hawkeye_health_check` to confirm the server is running, then `hawkeye_get_groups` to see what is indexed.
- **Opening files:** `hawkeye_execute_editor` works with any editor configured in Hawkeye. Call `hawkeye_get_editors` first to get the correct path and parameter format.
