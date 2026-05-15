# Storage setup

CrusPlayerKits uses two kinds of storage:

| Data | Storage location |
|---|---|
| Kit definitions | `kits.yml` |
| Player cooldowns | YAML, SQLite, or MySQL depending on `storage.type` |
| One-time kit claim records | YAML, SQLite, or MySQL depending on `storage.type` |
| Processed first-join category records | YAML, SQLite, or MySQL depending on `storage.type` |

Kit definitions remain in YAML. SQL storage is for player claim data, not for kit definitions.

## YAML storage

Default setup:

```yaml
storage:
  type: "yaml"
  kits-file: "kits.yml"
  player-data-file: "player_data.yml"
  auto-save-interval: 300
```

Generated files:

```text
plugins/CrusPlayerKits/kits.yml
plugins/CrusPlayerKits/player_data.yml
```

Use YAML for small and medium servers, simple setups, or development servers.

## SQLite storage

SQLite stores player claim data in a local `.db` file.

```yaml
storage:
  type: "sqlite"
  sqlite:
    file: "player_data.db"
```

Generated file:

```text
plugins/CrusPlayerKits/player_data.db
```

Use SQLite when you want a local database file without managing a MySQL server.

## MySQL storage

Use MySQL when multiple systems need database-backed player claim data or when you prefer central database management.

```yaml
storage:
  type: "mysql"
  table-prefix: "crusplayerkits"
  mysql:
    host: "127.0.0.1"
    port: 3306
    database: "minecraft"
    username: "minecraft_user"
    password: "replace-with-a-secure-password"
    use-ssl: false
    parameters: "useUnicode=true&characterEncoding=utf8&serverTimezone=UTC"
```

> [!WARNING]
> Never commit real MySQL usernames, passwords, hostnames, or production database names to a public repository.

## SQL tables

The table prefix is configurable:

```yaml
table-prefix: "crusplayerkits"
```

Default SQL tables:

```text
crusplayerkits_player_data
crusplayerkits_category_auto_claims
```

The player data table stores:

| Column | Purpose |
|---|---|
| `uuid` | Player UUID. |
| `kit` | Normalized kit name. |
| `cooldown_until` | Cooldown expiry as Unix seconds. |
| `one_shot` | One-time claim marker. |

The category auto-claim table stores:

| Column | Purpose |
|---|---|
| `uuid` | Player UUID. |
| `category` | Processed category ID. |

## Auto-save interval

```yaml
storage:
  auto-save-interval: 300
```

The value is in seconds. `300` means every 5 minutes.

Set it to `0` to disable scheduled auto-save. Manual saves still happen during plugin shutdown and reload flows.

## Fallback behavior

If SQL loading or saving fails, CrusPlayerKits attempts to fall back to YAML player data. This protects the server from losing all claim functionality during a database outage, but the console error should still be treated seriously.

## Migration notes

Recommended migration path:

1. Stop the server.
2. Back up the full plugin folder.
3. Configure the new `storage.type`.
4. Start the server and check console output.
5. Test `/kit claim`, cooldowns, one-shot kits, and first-join starter kits.
6. Keep the old backup until the new storage is confirmed stable.

Changing storage type does not automatically migrate old player data between YAML, SQLite, and MySQL. Plan the transition carefully if preserving cooldown history is required.
