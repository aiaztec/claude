# Git MCP – Claude Desktop Extension

A Claude Desktop extension that enables Git repository management using the official [mcp-server-git](https://github.com/modelcontextprotocol/servers/tree/main/src/git) package.

## Features

- Check repository status
- Stage files for commit
- Commit changes
- Show unstaged and staged diffs
- Compare branches or commits
- View commit history with optional date filtering
- Create and switch branches
- List local, remote or all branches
- Show commit contents

## Requirements

- **uv** installed and available in PATH as `uv.exe`
- **Git** installed and available in PATH as `git`
- Windows (win32)

## Installation

1. Download `git-mcp.dxt`
2. Open Claude Desktop → Settings → Extensions
3. Click **Install Extension** and select `git-mcp.dxt`
4. Restart Claude Desktop

> On first use, `uv.exe` will automatically download and install `mcp-server-git`. An internet connection is required for the first run.

## Tools

Each tool accepts `repo_path` (string) – absolute path to the local git repository.

| Tool | Description | Key parameters |
|---|---|---|
| `git_status` | Show working tree status | `repo_path` |
| `git_add` | Stage files | `repo_path`, `files` (array) |
| `git_commit` | Commit staged changes | `repo_path`, `message` |
| `git_diff_unstaged` | Show unstaged changes | `repo_path`, `context_lines` (optional) |
| `git_diff_staged` | Show staged changes | `repo_path`, `context_lines` (optional) |
| `git_diff` | Compare branches/commits | `repo_path`, `target` |
| `git_reset` | Unstage all changes | `repo_path` |
| `git_log` | Show commit history | `repo_path`, `max_count`, `start_timestamp`, `end_timestamp` |
| `git_create_branch` | Create new branch | `repo_path`, `branch_name`, `base_branch` (optional) |
| `git_checkout` | Switch branch | `repo_path`, `branch_name` |
| `git_show` | Show commit contents | `repo_path`, `revision` |
| `git_branch` | List branches | `repo_path`, `branch_type` (local/remote/all) |

## Note

`git_push` and `git_pull` are not included in `mcp-server-git`. These operations can be performed via Desktop Commander or a future custom wrapper.

## Compatibility

- Windows (win32)

## License

MIT
