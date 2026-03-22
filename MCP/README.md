# MCP – Model Context Protocol Extensions

This folder contains MCP server extensions for Claude Desktop in `.dxt` (Desktop Extension) format.

## What is MCP?

Model Context Protocol (MCP) is an open standard that allows Claude Desktop to connect to external tools, databases, and services. Each extension adds new capabilities directly accessible in Claude conversations.

## Available Extensions

### OracleSQLclMCP
**File:** `OracleSQLclMCP/oracle-sqlcl.dxt`

Connects Claude Desktop to an Oracle database using Oracle SQLcl's built-in MCP server.

- Create and manage named database connections
- Run SQL queries and view results
- Explore schemas, tables, and objects
- Execute async SQL jobs

See [OracleSQLclMCP/README.md](./OracleSQLclMCP/README.md) for setup and usage.

---

### GitMCP
**File:** `GitMCP/git-mcp.dxt`

Git repository management directly from Claude Desktop via the git command line.

See [GitMCP/README.md](./GitMCP/README.md) for setup and usage.

---

## Installation

1. Download the `.dxt` file from the desired subfolder
2. Open **Claude Desktop** → Settings → Extensions
3. Click **Install Extension** and select the `.dxt` file
4. Restart Claude Desktop

## Related

- [SKILLS/](../SKILLS/) – Reusable skill packages that complement these MCP extensions
