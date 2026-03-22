# Claude AI – Tools, Skills & Extensions

A personal repository for working with Claude AI. Contains MCP server extensions, Skills (reusable instruction sets for Claude Desktop), and automation resources built around Claude Desktop and the Anthropic ecosystem.

## Repository Structure

```
claude/
├── MCP/        # Model Context Protocol server extensions (.dxt format)
├── SKILLS/     # Reusable skill packages for Claude Desktop (.skill format)
└── README.md   # This file
```

---

## MCP – Model Context Protocol Extensions

Custom and curated MCP server extensions for Claude Desktop (`.dxt` format).
See [MCP/README.md](./MCP/README.md) for details.

| Extension | Description |
|---|---|
| [OracleSQLclMCP](./MCP/OracleSQLclMCP/) | Oracle database access via Oracle SQLcl built-in MCP server |
| [GitMCP](./MCP/GitMCP/) | Git repository management via git command line |

---

## SKILLS – Claude Desktop Skill Packages

Reusable skill packages (`.skill` files) for import into Claude Desktop.
Each `.skill` file is a zipped skill directory containing a `SKILL.md` instruction file and supporting assets.
See [SKILLS/README.md](./SKILLS/README.md) for details and import instructions.

| Skill | Description |
|---|---|
| [SQLcl](./SKILLS/SQLcl/) | Oracle database operations via SQLcl MCP |
| [SSH](./SKILLS/SSH/) | SSH connections to remote Linux servers with screen session support |

---

## Requirements

- [Claude Desktop](https://claude.ai/download)
- Individual requirements per extension/skill (see each folder's README)

## Installation

### MCP Extensions
1. Download the `.dxt` file from the desired extension folder
2. Open Claude Desktop → Settings → Extensions
3. Click **Install Extension** and select the `.dxt` file
4. Restart Claude Desktop

### Skills
1. Download the `.skill` file from the `SKILLS/` folder
2. Open Claude Desktop → Settings → Skills
3. Click **Import Skill** and select the `.skill` file

## License

MIT
