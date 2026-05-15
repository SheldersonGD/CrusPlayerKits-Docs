# Commands

Main command:

```text
/kit
```

Alias:

```text
/kits
```

Durations accept plain seconds or shorthand values:

```text
30
30s
5m
1h
1d
```

## Player commands

| Command | Permission | Description |
|---|---|---|
| `/kit` | `crusplayerkits.use` | Open the kit/category GUI. |
| `/kits` | `crusplayerkits.use` | Alias for `/kit`. |
| `/kit menu` | `crusplayerkits.use` | Open the kit/category GUI. |
| `/kit help` | `crusplayerkits.use` | Show available commands. |
| `/kit claim <kit>` | `crusplayerkits.use` + kit permission | Claim a kit directly without using the GUI. |
| `/kit list` | `crusplayerkits.use` | List all loaded kits. |
| `/kit info <kit>` | `crusplayerkits.use` | Show kit details: items, cooldown, one-shot state, permission, category, price, and command rewards. |
| `/kit preview <kit>` | `crusplayerkits.preview` | Open a read-only preview of a kit. |

## Admin commands

| Command | Permission | Description |
|---|---|---|
| `/kit create <kit> [cooldown|category] [oneshot] [category]` | `crusplayerkits.create` | Create a kit from the player inventory. |
| `/kit create <kit> --category <category>` | `crusplayerkits.create` | Create a kit and assign it to a category using a flag. |
| `/kit edit <kit>` | `crusplayerkits.edit` | Start an inventory-safe kit edit session. |
| `/kit edited` | `crusplayerkits.edit` | Save the active edit session. |
| `/kit editcancel` | `crusplayerkits.edit` | Cancel the active edit session and restore the original inventory. |
| `/kit editor <kit>` | `crusplayerkits.edit` | Open the in-game kit settings GUI. |
| `/kit settings <kit>` | `crusplayerkits.edit` | Alias for the kit settings GUI. |
| `/kit cooldown <kit> <seconds|5m|1h|1d>` | `crusplayerkits.edit` | Set a kit cooldown. |
| `/kit category <kit> <category>` | `crusplayerkits.edit` | Move a kit to a different category. |
| `/kit head set [kit]` | `crusplayerkits.edit` | Use the held player head as the kit GUI icon. |
| `/kit head remove [kit]` | `crusplayerkits.edit` | Reset the kit GUI icon to `CHEST`. |
| `/kit reward add <kit> <command>` | `crusplayerkits.edit` | Add a console command reward to a kit. |
| `/kit reward remove <kit> <index>` | `crusplayerkits.edit` | Remove a command reward by list index. |
| `/kit reward clear <kit>` | `crusplayerkits.edit` | Remove all command rewards from a kit. |
| `/kit reward list <kit>` | `crusplayerkits.edit` | List command rewards for a kit. |
| `/kit commands <add|remove|clear|list> <kit> ...` | `crusplayerkits.edit` | Alias for `/kit reward`. |
| `/kit price <kit> <amount|free>` | `crusplayerkits.price` | Set or clear a Vault economy price. |
| `/kit voucher get <kit> [amount]` | `crusplayerkits.voucher` | Create voucher items for yourself. |
| `/kit voucher give <player> <kit> [amount]` | `crusplayerkits.voucher` | Give voucher items to an online player. |
| `/kit give <player> <kit> [--rewards]` | `crusplayerkits.give` | Give a kit directly to an online player. |
| `/kit reset <player|uuid> <kit|all>` | `crusplayerkits.reset` | Reset cooldown and one-time claim data. |
| `/kit import essentials [file] [--overwrite]` | `crusplayerkits.import` | Import EssentialsX kits. |
| `/kit import playerkits [file] [--overwrite]` | `crusplayerkits.import` | Import PlayerKits kits. |
| `/kit delete <kit>` | `crusplayerkits.delete` | Delete a kit. Players receive a confirmation GUI; console must repeat the command within the confirmation window. |
| `/kit reload` | `crusplayerkits.reload` | Reload config, messages, categories, kits, economy state, and player data. |

## Create examples

Create a starter kit in the `starter` category:

```text
/kit create starter starter
```

Create a rank kit with a 1-day cooldown:

```text
/kit create warrior 1d false ranks
```

Create a one-time starter kit:

```text
/kit create welcome 0 true starter
```

Create with the category flag:

```text
/kit create recruit --category starter
```

## Reward command examples

Command rewards are executed by the server console after a successful claim.

```text
/kit reward add warrior eco give {player} 250
/kit reward add warrior lp user {player} permission set example.permission true
/kit reward list warrior
/kit reward remove warrior 1
```

Use `{player}` for the claiming player's name.

## Direct give examples

Give only the kit items:

```text
/kit give PlayerName warrior
```

Give the kit and execute command rewards:

```text
/kit give PlayerName warrior --rewards
```

## Reset examples

Reset one kit for a player:

```text
/kit reset PlayerName warrior
```

Reset all cooldowns, one-time claims, and category auto-claim markers for a player:

```text
/kit reset PlayerName all
```

UUIDs are accepted when the player is offline:

```text
/kit reset 00000000-0000-0000-0000-000000000000 all
```
