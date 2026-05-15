# Categories

Categories organize kits into a landing menu. They can control menu order, icon, lore, visibility permission, and first-join starter kit behavior.

Configuration path:

```yaml
categories:
  items:
    <category-id>:
      name: "..."
      material: "CHEST"
      lore: []
      priority: 1
      slot: 21
```

## Default category behavior

```yaml
categories:
  enabled: true
  default: "ranks"
  show-empty: false
```

| Path | Description |
|---|---|
| `categories.enabled` | Enables the category menu when there is more than one loaded category. |
| `categories.default` | Category used when a kit has no category. |
| `categories.show-empty` | Shows categories even if the player has no visible kits in them. |

Category IDs are normalized to lowercase and spaces become hyphens.

## Category item example

```yaml
categories:
  items:
    ranks:
      name: "<#C53131><bold>Rank Kits</bold>"
      material: "PLAYER_HEAD"
      lore:
        - " "
        - "<#797B87>| <#FAE0B2>Premium player kits."
        - "<#797B87>| <#FAE0B2>Available: <#FFC351>{available}<#797B87>/<#FFC351>{total}"
      priority: 2
      slot: 23
      permission: "server.kits.ranks"
```

| Option | Description |
|---|---|
| `name` | Display name in the category menu. |
| `material` | Bukkit material or supported custom head material spec. |
| `lore` | Category item lore. |
| `enchantment-glint-override` | Adds or removes the item glint. |
| `priority` | Sort order. Lower values appear earlier. |
| `slot` | Fixed category menu slot. Use `-1` for automatic placement. |
| `permission` | Optional visibility permission. |

## Moving kits between categories

Move an existing kit:

```text
/kit category warrior ranks
```

Create a kit directly in a category:

```text
/kit create warrior 1d false ranks
```

Create with a category flag:

```text
/kit create recruit --category starter
```

## Starter category and first-join auto-claim

CrusPlayerKits includes special first-join behavior for the `starter` category. This allows new players to automatically receive starter kits after joining.

Example:

```yaml
categories:
  items:
    starter:
      name: "<#AEFF51><bold>Starter Kits</bold>"
      material: "CHEST"
      priority: 1
      slot: 21
      auto-claim:
        first-join: true
        delay-ticks: 40
        only-new-players: true
        respect-category-permission: false
        respect-kit-permissions: false
        bypass-cooldown: false
        bypass-one-shot: false
        skip-price: true
        execute-rewards: true
        mark-processed-on-failure: false
        max-kits: 0
```

| Auto-claim option | Description |
|---|---|
| `first-join` | Enables first-join processing for the starter category. |
| `delay-ticks` | Delay after join before processing. `20` ticks is roughly one second. |
| `only-new-players` | Processes only players that have not joined before. |
| `respect-category-permission` | Requires the category permission before auto-claiming. |
| `respect-kit-permissions` | Requires each kit's claim permission before auto-claiming. |
| `bypass-cooldown` | Ignores cooldowns during auto-claim. |
| `bypass-one-shot` | Ignores one-time claim restrictions during auto-claim. |
| `skip-price` | Does not charge kit prices during auto-claim. |
| `execute-rewards` | Executes command rewards during auto-claim. |
| `mark-processed-on-failure` | Records the category as processed even if one or more grants fail. |
| `max-kits` | Maximum starter kits to process. `0` means no limit. |

## Recommended starter setup

Use a dedicated category for new-player kits:

```text
/kit create starter 0 true starter
/kit create food 12h false starter
```

Then test as a brand-new player. Do not test only with an operator account, because bypass permissions can hide configuration mistakes.

## Category troubleshooting

| Issue | Fix |
|---|---|
| Category does not appear | Check `categories.enabled`, `show-empty`, the category permission, and whether the player can see at least one kit in the category. |
| Kit appears in the wrong category | Run `/kit info <kit>` and check the `category` value. Move it with `/kit category <kit> <category>`. |
| Starter kit does not auto-claim | Check `starter.auto-claim.first-join`, `only-new-players`, kit permissions, inventory space, and console errors. |
| Player receives starter kits repeatedly | Check storage setup and whether category auto-claim data is saving correctly. |
