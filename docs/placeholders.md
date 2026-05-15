# PlaceholderAPI

CrusPlayerKits registers a PlaceholderAPI expansion when PlaceholderAPI is installed and enabled.

Identifier:

```text
crusplayerkits
```

## Global placeholders

| Placeholder | Description |
|---|---|
| `%crusplayerkits_total%` | Total loaded kits. |
| `%crusplayerkits_categories%` | Total loaded categories. |
| `%crusplayerkits_available%` | Number of kits currently available to the player. Requires a player context. |

## Kit placeholders

Replace `<kit>` with the kit name.

| Placeholder | Description |
|---|---|
| `%crusplayerkits_cooldown_<kit>%` | Player-specific remaining cooldown as a formatted duration. Without player context, returns the kit's base cooldown. |
| `%crusplayerkits_cooldown_seconds_<kit>%` | Player-specific remaining cooldown in seconds. |
| `%crusplayerkits_has_access_<kit>%` | `yes` if the player can access the kit, otherwise `no`. |
| `%crusplayerkits_claimed_<kit>%` | `yes` if the player already claimed a one-shot kit, otherwise `no`. |
| `%crusplayerkits_category_<kit>%` | Kit category ID. |
| `%crusplayerkits_price_<kit>%` | Formatted kit price. |
| `%crusplayerkits_commands_<kit>%` | Number of command rewards attached to the kit. |

Examples:

```text
%crusplayerkits_total%
%crusplayerkits_available%
%crusplayerkits_cooldown_warrior%
%crusplayerkits_has_access_warrior%
%crusplayerkits_price_warrior%
```

## Notes

- PlaceholderAPI must be installed before these placeholders can be used by other plugins.
- Player-specific placeholders need a player context. Console or global contexts may return neutral values.
- Kit names are resolved by CrusPlayerKits. Use the exact kit name shown by `/kit list`.
