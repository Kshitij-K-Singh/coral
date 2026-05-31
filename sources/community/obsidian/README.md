# Obsidian Local REST API (obsidian)

**Version:** 0.2.0
**Backend:** HTTP
**Tables:** 3
**Functions:** 2
**Base URL:** `https://127.0.0.1:27124`

Query notes, commands, tags, and search results from your Obsidian vault via the [Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api) plugin.

```bash
coral source add --file sources/community/obsidian/manifest.yaml
```

## Requirements

- Obsidian with the [Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api) plugin installed and enabled
- The plugin's API key (found in Settings → Local REST API)

## Tables

| Table | Description |
|-------|-------------|
| `commands` | Available Obsidian command palette actions |
| `tags` | Tags across the vault with usage counts |
| `vault_files` | Files and folders at the vault root |

## Functions

| Function | Description |
|----------|-------------|
| `search(query)` | Fuzzy search notes by keyword (returns ranked results with scores) |
| `read_note(path)` | Read a note as structured JSON with content, tags, and frontmatter |
| `list_directory(path)` | List files and folders in a vault directory |

## Example Queries

### List available commands

```sql
SELECT id, name FROM obsidian.commands LIMIT 20
```

### List all tags with usage counts

```sql
SELECT tag, count FROM obsidian.tags ORDER BY count DESC
```

### Search notes

```sql
SELECT filename, score FROM obsidian.search(query => 'project notes') LIMIT 10
```

### List files at vault root

```sql
SELECT name FROM obsidian.vault_files
```

### List files in a subdirectory

```sql
SELECT name FROM obsidian.list_directory(path => 'projects')
```

### Read a note by path

```sql
SELECT content FROM obsidian.read_note(path => 'daily/2024-01-15.md')
```

### Read note metadata

```sql
SELECT path, tags, frontmatter FROM obsidian.read_note(path => 'meeting-notes.md')
```

## Quick start

```bash
# Confirm connectivity
coral sql "SELECT id, name FROM obsidian.commands LIMIT 1"

# List all tags in your vault
coral sql "SELECT tag, count FROM obsidian.tags ORDER BY count DESC LIMIT 10"

# Search for notes about a topic
coral sql "SELECT filename, score FROM obsidian.search(query => 'meeting') LIMIT 10"

# Read a specific note
coral sql "SELECT content FROM obsidian.read_note(path => 'projects/README.md')"
```

## Notes

- The API runs locally on your machine. Use `http://127.0.0.1:27123` for HTTP or `https://127.0.0.1:27124` for HTTPS.
- If HTTPS fails due to the self-signed certificate, use the HTTP URL instead.
- The API key grants full access to your vault. Use a dedicated vault if needed.
- See the [API documentation](https://coddingtonbear.github.io/obsidian-local-rest-api/) for full details.
