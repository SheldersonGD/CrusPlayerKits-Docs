# Configuration

Main configuration file:

```text
plugins/CrusPlayerKits/config.yml
```

Message file:

```text
plugins/CrusPlayerKits/messages.yml
```

Kit definitions:

```text
plugins/CrusPlayerKits/kits.yml
```

> [!IMPORTANT]
> Back up the plugin folder before editing production configuration. Do not commit production player data, SQL credentials, or private server details to a public repository.

## General settings

```yaml
general:
  debug: false
  max-kit-name-length: 32
```

| Path | Type | Description |
|---|---|---|
| `general.debug` | boolean | Enables additional console logging. Keep disabled unless debugging. |
| `general.max-kit-name-length` | number | Maximum kit name length. Kit names must use letters, numbers, underscores, or hyphens. |

## Storage settings

```yaml
storage:
  kits-file: "kits.yml"
  player-data-file: "player_data.yml"
  auto-save-interval: 300
  type: "yaml"
  table-prefix: "crusplayerkits"
```

| Path | Type | Description |
|---|---|---|
| `storage.kits-file` | string | YAML file used for kit definitions. |
| `storage.player-data-file` | string | YAML file used for player claim data when `type` is `yaml`. |
| `storage.auto-save-interval` | seconds | Auto-save interval for player data. Set to `0` to disable scheduled auto-save. |
| `storage.type` | string | `yaml`, `sqlite`, or `mysql`. |
| `storage.table-prefix` | string | Prefix for SQL tables. Invalid characters are sanitized to underscores. |

See [Storage setup](storage-setup.md) for full YAML, SQLite, and MySQL examples.

## Economy settings

```yaml
economy:
  enabled: true
  require-vault: false
```

| Path | Type | Description |
|---|---|---|
| `economy.enabled` | boolean | Enables the Vault economy hook. |
| `economy.require-vault` | boolean | Logs a warning when Vault is missing and economy is expected. |

Paid kits require Vault and an economy provider. If the provider is missing, paid claims are blocked instead of being granted for free.

## Voucher settings

```yaml
vouchers:
  enabled: true
  redeem:
    bypass-permission: true
    bypass-cooldown: true
    bypass-one-shot: true
    charge-price: false
```

| Path | Type | Description |
|---|---|---|
| `vouchers.enabled` | boolean | Allows voucher redemption. Existing voucher items remain marked but cannot redeem while disabled. |
| `vouchers.redeem.bypass-permission` | boolean | Voucher redemption ignores the kit permission. |
| `vouchers.redeem.bypass-cooldown` | boolean | Voucher redemption ignores cooldowns. |
| `vouchers.redeem.bypass-one-shot` | boolean | Voucher redemption ignores one-time claim limits. |
| `vouchers.redeem.charge-price` | boolean | Charges the kit price when redeeming a voucher. |

See [Vouchers](vouchers.md) for item customization and redemption behavior.

## Claim behavior

```yaml
claim:
  auto-armor: true
  auto-offhand: true
  drop-if-full: false
  sound-success: "ENTITY_PLAYER_LEVELUP"
  sound-fail: "ENTITY_VILLAGER_NO"
```

| Path | Type | Description |
|---|---|---|
| `claim.auto-armor` | boolean | Automatically places armor items into armor slots where possible. |
| `claim.auto-offhand` | boolean | Automatically places offhand item where possible. |
| `claim.drop-if-full` | boolean | Drops overflow items instead of failing when inventory space is insufficient. |
| `claim.sound-success` | sound name | Sound played after a successful claim. |
| `claim.sound-fail` | sound name | Sound played after a failed claim. |
| `claim.sound-*-volume` | decimal | Sound volume. |
| `claim.sound-*-pitch` | decimal | Sound pitch. |

## Edit session safety

```yaml
edit:
  block-item-drop: true
  cancel-on-world-change: true
  backup-file: "edit_backups.yml"
```

| Path | Type | Description |
|---|---|---|
| `edit.block-item-drop` | boolean | Blocks item dropping while editing a kit. |
| `edit.cancel-on-world-change` | boolean | Cancels an edit session if the editor changes world. |
| `edit.backup-file` | string | File used for edit-session inventory backups. |

Editing a kit temporarily replaces the admin's inventory. CrusPlayerKits backs up the original inventory and restores it when the session is saved, cancelled, or recovered.

## Category settings

```yaml
categories:
  enabled: true
  default: "ranks"
  show-empty: false
```

| Path | Type | Description |
|---|---|---|
| `categories.enabled` | boolean | Enables the category landing page when more than one category exists. |
| `categories.default` | string | Default category used for newly created or uncategorized kits. |
| `categories.show-empty` | boolean | Shows categories even when they contain no visible kits. |

See [Categories](categories.md) for complete examples.

## Menu settings

The main menu supports configurable title, size, sounds, filler item, info item, and navigation items.

```yaml
menu:
  title: "&#C53131&lᴋɪᴛs &#797B87| &#FAE0B2{category} &#797B87({page}/{pages})"
  size: 54
  sound-click: "UI_BUTTON_CLICK"
  sound-open: "BLOCK_AMETHYST_CLUSTER_FALL"
```

Common placeholders inside GUI text:

| Placeholder | Meaning |
|---|---|
| `{player}` | Player name. |
| `{category}` | Current category. |
| `{page}` | Current page. |
| `{pages}` | Total pages. |
| `{total}` | Total kit count in the current context. |
| `{available}` | Available kits in the current category context. |
| `{kit}` | Kit name, where supported. |
| `{price}` | Formatted kit price, where supported. |

## Text formatting

CrusPlayerKits supports MiniMessage-style formatting and legacy color codes in configured text.

Examples:

```yaml
name: "<#FFC351><bold>Starter Kit</bold>"
name: "&#FFC351&lStarter Kit"
```

Use a consistent style across menus, voucher names, and messages for a polished result.

## Reloading

After editing config files, run:

```text
/kit reload
```

This reloads config, messages, categories, kits, economy state, and player data. Use a full restart after changing plugin versions, storage drivers, dependencies, or server software.
