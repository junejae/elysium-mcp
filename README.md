# Elysium MCP

MCP (Model Context Protocol) server for Obsidian-based Second Brain with AI-powered semantic search.

## Features

- **Semantic Search**: Find related notes using AI-powered embeddings (local HTP - no external API required)
- **Vault Management**: Validate schemas, audit policies, check vault health
- **MCP Integration**: Works with Claude Desktop, Claude Code, and other MCP clients

## Installation

### From Source

```bash
git clone https://github.com/junejae/elysium-mcp.git
cd elysium-mcp
cargo build --release
```

### From crates.io (coming soon)

```bash
cargo install elysium-mcp
```

## Usage

### CLI Commands

```bash
# Validate vault schema
elysium validate

# Run comprehensive audit
elysium audit

# Check vault health (0-100 score)
elysium health

# Semantic search
elysium semantic-search "your query"

# Find related notes
elysium related "note-name"

# Index notes for semantic search
elysium index
```

### MCP Server

Start the MCP server for Claude Desktop or other MCP clients:

```bash
elysium mcp
```

#### Claude Desktop Configuration

Add to your Claude Desktop config (`~/.config/claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "elysium": {
      "command": "/path/to/elysium",
      "args": ["mcp"],
      "cwd": "/path/to/your/vault"
    }
  }
}
```

### MCP Tools

| Tool | Description |
|------|-------------|
| `vault_search` | Semantic search using gist embeddings |
| `vault_get_note` | Get note content and metadata |
| `vault_list_notes` | List notes with type/area filters |
| `vault_health` | Get vault health score (0-100) |
| `vault_status` | Get note counts by type/area |
| `vault_audit` | Run policy compliance audit |

## Vault Structure

Elysium expects an Obsidian vault with the following structure:

```
vault/
├── Notes/          # All notes (flat, no subfolders)
├── Projects/       # Active projects
├── Archive/        # Completed projects
├── _system/        # Dashboards, templates
└── inbox.md        # Quick capture
```

### YAML Schema

Notes should have frontmatter with these fields:

```yaml
type: note | term | project | log
status: active | done | archived
area: work | tech | life | career | learning | reference
gist: >
  2-3 sentence summary (max 100 words)
tags: [lowercase, flat, max_5]
```

## Technical Details

- **Embeddings**: Uses HTP (Harmonic Token Projection) - a local, training-free embedding method
- **Storage**: SQLite for vector storage and full-text search
- **Protocol**: MCP over stdio (no network ports)

## Related Projects

- [Elysium](https://github.com/junejae/elysium) - Obsidian plugin (coming soon)

## License

MIT
