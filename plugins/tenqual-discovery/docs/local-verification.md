# Local Verification

This document records the local verification target for the Tenqual Claude plugin package.

## Preconditions

- Claude Code is installed.
- The plugin package is checked out locally.
- The hosted MCP endpoint is declared in `.mcp.json`.
- The package contains no hooks, executables, telemetry, credential readers, or undeclared network destinations.

## Validation Commands

Run this check from the plugin root:

```bash
claude plugin validate . --strict
```

If Claude Code is installed outside the shell path, use the absolute path:

```bash
$HOME/.local/bin/claude plugin validate . --strict
```

## Expected Result

```text
Validating plugin manifest: .../.claude-plugin/plugin.json
Validation passed
```

## Manual Review Before Submission

- Confirm the production MCP endpoint has been scanned and exercised in MCP Inspector.
- Confirm every MCP tool has accurate OAuth security metadata and tool annotations.
- Confirm missing scopes return `_meta["mcp/www_authenticate"]`.
- Confirm the default OAuth grant remains read-oriented.
- Confirm a synthetic reviewer workspace is available.
- Confirm privacy, support, and setup documentation are public.
- Confirm the release commit matches the production API revision tested.
