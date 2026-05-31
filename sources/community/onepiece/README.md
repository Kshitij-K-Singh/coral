# One Piece API (onepiece)

**Version:** 0.1.0
**Backend:** HTTP
**Tables:** 1
**Base URL:** `https://api.api-onepiece.com/v2`

Query Devil Fruits from the One Piece API. No authentication required.

```bash
coral source add --file sources/community/onepiece/manifest.yaml
```

## Tables

| Table | Description |
|-------|-------------|
| `fruits` | Devil Fruits catalog entries with names, types, and descriptions |

### `fruits`

| Column | Type | Description |
|--------|------|-------------|
| `id` | Int64 | Devil Fruit identifier |
| `name` | Utf8 | Localized Devil Fruit name |
| `description` | Utf8 | Devil Fruit description text |
| `roman_name` | Utf8 | Romanized Devil Fruit name |
| `type` | Utf8 | Fruit type (Paramecia, Logia, Zoan, etc.) |
| `image_url` | Utf8 | Public image URL for the Devil Fruit |

## Example Queries

### List all Devil Fruits

```sql
SELECT id, name, type FROM onepiece.fruits LIMIT 10
```

### Find fruits by type

```sql
SELECT name, roman_name, description
FROM onepiece.fruits
WHERE type = 'Logia'
```

### Get fruit details

```sql
SELECT name, description, image_url
FROM onepiece.fruits
WHERE id = 1
```

### List all fruit types

```sql
SELECT DISTINCT type FROM onepiece.fruits
```

## Quick start

```bash
# List all Devil Fruits
coral sql "SELECT name, type FROM onepiece.fruits LIMIT 5"

# Find all Paramecia fruits
coral sql "SELECT name, roman_name FROM onepiece.fruits WHERE type = 'Paramecia' LIMIT 10"
```

## Notes

- The API is a fan-maintained service and may not be stable.
- Some fields like `description`, `roman_name`, `type`, and `image_url` may be null.
- No authentication is required to use this API.
