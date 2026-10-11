# Changelog

## [1.0.6] - 2026-10-11

Changed:

- Server `instructions` in the MCP `initialize` response, rewritten tool descriptions and skill: generic "where is X defined" lookups now go to Hawkeye first.
- `docs/tools.md` now documents `hawkeye_expand_context` and Hawkeye query syntax (unquoted words = separate terms, `"quoted"` = exact phrase, `.ext`, `-term`).

Fixed:

- `hawkeye_expand_context` no longer fails the whole call when a hit's line is past the end of its file.

## [1.0.5] - 2026-09-28

Added:

- Unity/Unreal Engine projects now use Hawkeye search by default — guidance for `.meta`/guid lookups, prefabs, ScriptableObjects, Blueprints, and `.uasset`/`.umap` files, alongside existing code search.
- `hawkeye_reload_index` tool, documented in `docs/tools.md`: triggers a headless Hawkeye index reload (no window, doesn't steal focus) on request, without needing to launch the full Hawkeye GUI.

## [0.1.0] - 2026-05-26

Initial public documentation and MCP configuration examples for Hawkeye AI Bridge.

Added:

- VS Code MCP examples.
- Claude Desktop MCP example placeholder.
- Clade CLI example.
- Troubleshooting guide.
- Privacy and security notes.
- Public repository structure for discovery and setup.
