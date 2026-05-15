# CrusPlayerKits Documentation

CrusPlayerKits is a modern player kits plugin designed for Paper, Purpur, and Folia servers. It provides a polished GUI workflow for claiming, previewing, editing, pricing, importing, and distributing kits without forcing server owners to manage everything by hand in YAML.

> [!IMPORTANT]
> This repository is documentation-only. Do not commit private server files, database credentials, production player data, or paid plugin binaries here.

## What CrusPlayerKits includes

| Area | Summary |
|---|---|
| Kit menus | Category-based GUI menus with pagination, filler items, info items, preview support, and custom icons. |
| Admin tools | In-game kit creation, inventory-safe editing sessions, cooldown/category/reward/price management, delete confirmation, and reload support. |
| Claim control | Per-kit permissions, cooldowns, one-time kits, bypass permissions, direct claiming, and first-join starter kits. |
| Economy | Vault-backed paid kits with per-kit prices and payment rollback when a claim fails. |
| Vouchers | Physical kit voucher items using persistent item data, configurable appearance, and configurable redemption rules. |
| Storage | YAML by default, with SQLite and MySQL support for player claim data. |
| Importers | EssentialsX and PlayerKits conversion commands with overwrite support. |
| Integrations | PlaceholderAPI placeholders and optional Vault economy support. |

## Compatibility

| Requirement | Value |
|---|---|
| Java | 21 or newer |
| Server software | Paper, Purpur, or Folia |
| Minecraft API target | 1.21.x |
| Optional dependencies | PlaceholderAPI, Vault, a Vault-compatible economy plugin |

Paper/Purpur/Folia are the intended platforms. Spigot/Bukkit compatibility is not guaranteed because the plugin is built against Paper API and declares Folia support.

## Documentation index

| Guide | Purpose |
|---|---|
| [Installation guide](docs/installation.md) | Install the plugin, optional hooks, and verify startup. |
| [Commands](docs/commands.md) | Full command list with syntax, permissions, and examples. |
| [Permissions](docs/permissions.md) | Permission nodes for players, staff, admins, and paid-kit bypasses. |
| [Configuration](docs/configuration.md) | Main `config.yml` sections and safe editing practices. |
| [Categories](docs/categories.md) | Category menus, category permissions, and first-join starter kits. |
| [Vouchers](docs/vouchers.md) | Voucher commands, redemption behavior, and item customization. |
| [Economy prices](docs/economy-prices.md) | Vault setup, paid kit behavior, and price commands. |
| [Storage setup](docs/storage-setup.md) | YAML, SQLite, and MySQL player data storage. |
| [Importers](docs/importers.md) | Import kits from EssentialsX or PlayerKits. |
| [Troubleshooting](docs/troubleshooting.md) | Common setup, claim, economy, storage, and importer issues. |
| [PlaceholderAPI](docs/placeholders.md) | Built-in placeholders for scoreboards, menus, and chat plugins. |
| [Upload to GitHub](UPLOAD_TO_GITHUB.md) | How to push this documentation to the docs repository. |

## Recommended first setup

1. Install the plugin on a test server first.
2. Start the server once to generate the default files.
3. Configure categories, storage, economy, and voucher behavior.
4. Create or import kits.
5. Assign permissions with your permissions plugin.
6. Test kit claiming as a normal player, not only as an operator.

## Quick command examples

```text
/kit
/kit create starter starter
/kit create warrior 1d false ranks
/kit price warrior 5000
/kit voucher give PlayerName warrior 1
/kit import essentials plugins/Essentials/kits.yml --overwrite
/kit reload
```

## Safe documentation policy

Keep this repository clean and public-safe:

- Do not upload `player_data.yml`, `player_data.db`, SQL dumps, or production backups.
- Do not upload MySQL passwords or hosting details.
- Do not upload private server IPs, staff notes, license keys, or customer information.
- Do not upload the compiled plugin JAR unless the repository is intentionally private and distribution is allowed.
- Use example values in documentation instead of real credentials.

