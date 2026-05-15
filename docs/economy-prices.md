# Economy prices

CrusPlayerKits can charge players for claiming kits using Vault and a Vault-compatible economy provider.

## Requirements

| Component | Required for paid kits |
|---|---:|
| Vault | Yes |
| Vault-compatible economy plugin | Yes |
| `economy.enabled: true` | Yes |

Configuration:

```yaml
economy:
  enabled: true
  require-vault: false
```

`require-vault` does not install Vault. It only makes the missing Vault state explicit in console logs.

## Set kit prices

Set a price:

```text
/kit price <kit> <amount>
```

Examples:

```text
/kit price warrior 5000
/kit price vip 12500.50
```

Make a kit free:

```text
/kit price warrior free
```

Accepted free values:

```text
free
none
0
```

Permission:

```text
crusplayerkits.price
```

## Claim behavior for paid kits

When a player claims a paid kit:

1. CrusPlayerKits checks kit permission.
2. It checks one-shot and cooldown rules.
3. It checks that economy support is available.
4. It checks the player's balance.
5. It withdraws the price.
6. It gives the kit.
7. It records cooldown and one-shot data after a successful grant.
8. It executes command rewards.

If the inventory grant fails after payment, the plugin attempts to refund the player.

## Bypass price permission

Players with this permission can claim paid kits without being charged:

```text
crusplayerkits.bypass.price
```

Full admins also bypass normal claim restrictions:

```text
crusplayerkits.admin
```

## Economy unavailable behavior

If a kit has a price above `0` and economy support is unavailable, the paid claim is blocked. The plugin does not silently give paid kits for free.

Common causes:

- Vault is not installed.
- No Vault-compatible economy provider is installed.
- The economy plugin loaded after Vault incorrectly.
- `economy.enabled` is set to `false`.

## Voucher interaction

Vouchers have their own setting:

```yaml
vouchers:
  redeem:
    charge-price: false
```

When `charge-price` is `false`, vouchers redeem without charging the kit price. When `true`, voucher redemption uses the same economy checks as normal paid claims.

## Best practices

- Keep all paid-kit prices in game using `/kit price` or review `kits.yml` carefully.
- Test with a non-operator account.
- Do not give `crusplayerkits.bypass.price` to normal players.
- Use `require-vault: true` on production servers where paid kits are mandatory, so missing economy support is obvious during startup.
