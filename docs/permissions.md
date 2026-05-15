# Permissions

CrusPlayerKits uses command permissions, bypass permissions, and per-kit claim permissions.

## Recommended permission groups

### Default players

```text
crusplayerkits.use
crusplayerkits.preview
crusplayerkits.kit.<kit>
```

### Moderators

```text
crusplayerkits.use
crusplayerkits.preview
crusplayerkits.give
crusplayerkits.reset
```

### Kit managers

```text
crusplayerkits.create
crusplayerkits.edit
crusplayerkits.delete
crusplayerkits.price
crusplayerkits.voucher
crusplayerkits.import
crusplayerkits.reload
```

### Full admins

```text
crusplayerkits.admin
```

## Permission reference

| Permission | Default | Description |
|---|---:|---|
| `crusplayerkits.use` | `true` | Open the kit menu and use basic kit commands. |
| `crusplayerkits.preview` | `true` | Preview kits in a read-only GUI. |
| `crusplayerkits.create` | `op` | Create kits from the player's inventory. |
| `crusplayerkits.edit` | `op` | Edit kit contents, GUI icons, cooldowns, categories, and command rewards. |
| `crusplayerkits.delete` | `op` | Delete kits. |
| `crusplayerkits.reload` | `op` | Reload plugin configuration and data. |
| `crusplayerkits.import` | `op` | Import kits from supported plugins. |
| `crusplayerkits.give` | `op` | Give kits directly to online players. |
| `crusplayerkits.reset` | `op` | Reset player cooldowns and one-time kit claims. |
| `crusplayerkits.voucher` | `op` | Create and give physical kit vouchers. |
| `crusplayerkits.price` | `op` | Manage per-kit economy prices. |
| `crusplayerkits.bypass.cooldown` | `op` | Ignore kit cooldowns. |
| `crusplayerkits.bypass.oneshot` | `op` | Claim one-shot kits more than once. |
| `crusplayerkits.bypass.price` | `op` | Claim paid kits without being charged. |
| `crusplayerkits.admin` | `op` | Full administrative access. Includes the documented admin permissions. |

## Per-kit claim permissions

Every kit has its own claim permission:

```text
crusplayerkits.kit.<kit>
```

Examples:

```text
crusplayerkits.kit.starter
crusplayerkits.kit.warrior
crusplayerkits.kit.warden
```

A legacy alias is also accepted:

```text
crusplayerkits.claim.<kit>
```

Use the modern `crusplayerkits.kit.<kit>` node for new setups.

## Category permissions

Categories may define an optional permission in `config.yml`:

```yaml
categories:
  items:
    ranks:
      permission: "server.kits.ranks"
```

When set, players need that category permission to see the category unless they have `crusplayerkits.admin`.

Category permissions control category visibility. Kit claiming is still controlled by the kit's own permission unless a special claim flow bypasses permission checks, such as configurable voucher or first-join behavior.

## Bypass behavior

| Permission | Applies to | Behavior |
|---|---|---|
| `crusplayerkits.bypass.cooldown` | Normal kit claims | Cooldowns are ignored. |
| `crusplayerkits.bypass.oneshot` | Normal kit claims | One-time claim limits are ignored. |
| `crusplayerkits.bypass.price` | Normal paid kit claims | The player is not charged. |
| `crusplayerkits.admin` | Most checks | Grants admin command access and bypasses normal claim restrictions. |

## Security notes

- Do not give `crusplayerkits.admin` to broad staff groups.
- Do not give `crusplayerkits.bypass.price` to normal players if paid kits matter.
- Test permissions with a non-operator account. Operators can bypass many issues during testing.
