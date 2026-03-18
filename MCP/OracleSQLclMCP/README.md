# Oracle SQLcl MCP – Claude Desktop Extension

A Claude Desktop extension that enables Oracle database access via Oracle SQLcl's built-in MCP server.

## Features

- List saved SQLcl named connections
- Connect to Oracle databases using named connections
- Execute SQL and PL/SQL queries
- Execute SQLcl-specific commands (INFO, DESC, CTAS...)
- Disconnect from database session

## Requirements

- **Oracle SQLcl 25.2+** installed and available in PATH as `sql`
- **Java 17+ JRE** installed
- **Named connections** configured in SQLcl with saved passwords

## Installation

1. Download `oracle-sqlcl.dxt`
2. Open Claude Desktop → Settings → Extensions
3. Click **Install Extension** and select `oracle-sqlcl.dxt`
4. Restart Claude Desktop

## Setting up Named Connections in SQLcl

To create a named connection with a saved password, import connections from SQL Developer export file:

```sql
SQL> CONNMGR IMPORT myconns.json
```

To list existing named connections:

```sql
SQL> CONNMGR LIST
```

To show details of a specific connection:

```sql
SQL> CONNMGR SHOW MyConnection
```

To test a connection:

```sql
SQL> CONNMGR TEST MyConnection
```

## Tools

| Tool | Description |
|---|---|
| `list-connections` | List all saved named connections |
| `connect` | Connect to a named connection |
| `run-sql` | Execute SQL or PL/SQL |
| `run-sqlcl` | Execute SQLcl-specific commands |
| `disconnect` | Disconnect current session |

## Compatibility

- Windows (win32)

## License

MIT
