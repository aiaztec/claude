# SKILLS – Claude Desktop Skill Packages

This folder contains reusable skill packages for Claude Desktop in `.skill` format.

## What is a Skill?

A **Skill** is a packaged set of instructions that tells Claude *how* to perform a specific task — which tools to use, in what order, with what logic. Skills are stored as `.skill` files, which are zipped archives of a skill directory containing:

- `SKILL.md` – the main instruction file read by Claude
- Supporting assets, reference docs, and scripts (where applicable)

## Available Skills

### SQLcl
**File:** `SQLcl.skill`  
**Source folder:** `SQLcl/`

Covers all Oracle database operations via the SQLcl MCP server:
- Creating and managing named database connections (with interactive form widget)
- Running SQL queries and async jobs
- Exploring schemas and database objects

**Triggers:** "vytvor spojenie", "pripoj sa", "spusti SQL", "zobraz tabuľky", "Oracle databáza", "SQLcl", "create connection", "run query"

---

### SSH
**File:** `SSH.skill`  
**Source folder:** `SSH/`

SSH connections to remote Linux servers from Claude Desktop using Desktop Commander.  
Supports two modes:
- **Screen mode** – for long-running tasks and interactive work via GNU screen
- **Direct mode** – for simple one-off commands

**Triggers:** "connect to server", "pripoj sa na server", "screen session", "run command on server", "spusti na serveri"

---

## How to Import a Skill

1. Download the `.skill` file from this folder
2. Open **Claude Desktop** → Settings → Skills
3. Click **Import Skill** and select the `.skill` file
4. The skill is now available in your Claude Desktop sessions

## How `.skill` Files Are Created

Each `.skill` file is created by zipping the corresponding skill subfolder:

```
# Example: creating SQLcl.skill
Compress-Archive -Path SKILLS\SQLcl -DestinationPath SKILLS\SQLcl.skill
```

## Related

- [MCP/](../MCP/) – MCP extensions that these skills are designed to work with
