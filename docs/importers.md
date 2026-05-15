# Importers

CrusPlayerKits can import kits from EssentialsX and PlayerKits YAML files. Importers are best-effort converters: review every imported kit in game before using it on production.

## Supported import commands

EssentialsX:

```text
/kit import essentials [file] [--overwrite]
```

PlayerKits:

```text
/kit import playerkits [file] [--overwrite]
```

Permission:

```text
crusplayerkits.import
```

## Default import paths

EssentialsX default lookup:

```text
plugins/Essentials/kits.yml
plugins/Essentials/config.yml
```

PlayerKits default lookup:

```text
plugins/PlayerKits/kits.yml
```

Examples:

```text
/kit import essentials
/kit import essentials plugins/Essentials/kits.yml --overwrite
/kit import playerkits
/kit import playerkits plugins/PlayerKits/kits.yml --overwrite
```

## Overwrite behavior

Without `--overwrite`, existing CrusPlayerKits kits are skipped.

With `--overwrite`, imported kits with matching names replace existing kits.

```text
/kit import essentials plugins/Essentials/kits.yml --overwrite
```

## Imported kit defaults

Imported kits receive safe CrusPlayerKits defaults:

| Property | Default behavior |
|---|---|
| Kit name | Unsafe characters are replaced with underscores. |
| Permission | `crusplayerkits.kit.<kit>` |
| Category | `imported` unless the source provides a category. |
| Price | `0.0` |
| Menu icon | Selected from common kit-name hints, otherwise `CHEST`. |
| Menu priority | High numeric priority so imported kits appear after curated kits. |

## EssentialsX import behavior

The Essentials importer reads kit sections and supports common kit item formats, including:

- Human-readable item lines.
- Bukkit serialized item maps or sections.
- Command lines starting with `/`, `cmd:`, or `command:`.
- Common material aliases.
- Legacy numeric material IDs for common items.
- Common enchantment aliases.

Essentials delay behavior:

| Source value | Result |
|---|---|
| `delay` or `cooldown` greater than `0` | Kit cooldown in seconds. |
| Negative delay | Imported as a one-shot kit. |
| Missing delay | No cooldown. |

## PlayerKits import behavior

The PlayerKits importer checks multiple common field names for compatibility:

| Data | Supported source keys |
|---|---|
| Cooldown | `cooldown-seconds`, `cooldown_seconds`, `cooldown`, `delay`, `claim_cooldown` |
| One-shot | `one-shot`, `one_shot`, `one_time`, `one-time`, `oneTime` |
| Category | `category` |
| Commands | `command-rewards`, `commands`, `actions`, `claim-actions`, `actions_on_claim` |
| Items | `main`, `items`, `content`, `inventory`, `contents` |

## Item line support

Human-readable imported item lines may include:

```text
slot:0 DIAMOND_SWORD 1 sharpness:5 unbreaking:3 name:&bStarter_Blade
GOLDEN_APPLE 8
cmd: eco give {player} 100
```

Supported token patterns include:

| Token | Meaning |
|---|---|
| `slot:<number>` | Target inventory slot. |
| `<material>` | Bukkit material, supported alias, or supported legacy numeric ID. |
| `<amount>` | Item amount. |
| `name:<text>` | Display name. Underscores become spaces. |
| `lore:<line1|line2>` | Lore lines separated by `|`. |
| `player:<name>` | Skull owner for player heads. |
| `title:<text>` | Written book title. |
| `author:<text>` | Written book author. |
| `color:r,g,b` | Leather armor color. |
| `custom_model_data:<number>` | Custom model data. |
| `<enchantment>:<level>` | Enchantment level. |

Command placeholders from common source formats are normalized to:

```text
{player}
```

## Recommended import workflow

1. Back up `plugins/CrusPlayerKits/`.
2. Run the import on a test server first.
3. Review the console summary: imported, skipped, failed.
4. Open `/kit` and inspect categories.
5. Use `/kit preview <kit>` for every important kit.
6. Use `/kit editor <kit>` to fix icon, lore, category, cooldown, or price.
7. Test claiming as a normal player.
8. Use `--overwrite` only after you are sure the imported result is correct.

## Import troubleshooting

| Result | Meaning | Fix |
|---|---|---|
| `File not found` | The target file does not exist on disk. | Provide the correct path or place the old plugin's file in its expected folder. |
| `No kits section found` | Essentials config does not contain a `kits` section. | Use the correct Essentials file. |
| `failed` count is high | Some item formats could not be parsed. | Review console warnings and manually recreate unsupported custom items. |
| Imported kits are hidden | Player lacks `crusplayerkits.kit.<kit>` or category visibility permission. | Assign permissions and check `/kit info <kit>`. |
