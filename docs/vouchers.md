# Vouchers

Vouchers are physical items that redeem a configured kit when right-clicked. They are marked internally with persistent item data, so players cannot create valid vouchers by only renaming a normal item.

## Commands

Give yourself vouchers:

```text
/kit voucher get <kit> [amount]
```

Give vouchers to an online player:

```text
/kit voucher give <player> <kit> [amount]
```

Examples:

```text
/kit voucher get warrior 3
/kit voucher give PlayerName starter 1
```

Permission:

```text
crusplayerkits.voucher
```

Voucher stack amounts are clamped to a safe stack size.

## Redemption behavior

Players redeem a voucher by right-clicking it in their main hand.

Default behavior:

```yaml
vouchers:
  enabled: true
  redeem:
    bypass-permission: true
    bypass-cooldown: true
    bypass-one-shot: true
    charge-price: false
```

| Option | Default | Description |
|---|---:|---|
| `vouchers.enabled` | `true` | Enables voucher redemption. |
| `vouchers.redeem.bypass-permission` | `true` | The voucher can redeem even if the player lacks the kit permission. |
| `vouchers.redeem.bypass-cooldown` | `true` | The voucher can redeem while the kit is on cooldown. |
| `vouchers.redeem.bypass-one-shot` | `true` | The voucher can redeem even if the player already claimed a one-shot kit. |
| `vouchers.redeem.charge-price` | `false` | The player is not charged the kit's economy price by default. |

If redemption succeeds, one voucher is consumed. If the claim fails, the voucher stack is restored.

## Voucher item customization

```yaml
vouchers:
  item:
    material: "PAPER"
    name: "<#FFC351><bold>Kit Voucher</bold> <gray>|</gray> <#FAE0B2>{kit}"
    lore:
      - " "
      - "<#797B87>| <#FAE0B2>Right-click to redeem."
      - "<#797B87>| <#FAE0B2>Kit: <#FFC351>{kit}"
      - "<#797B87>| <#FAE0B2>Price: <#FFC351>{price}"
      - " "
    enchantment-glint-override: true
```

Supported placeholders in voucher text:

| Placeholder | Meaning |
|---|---|
| `{kit}` | Kit name. |
| `{category}` | Kit category. |
| `{price}` | Formatted kit price. |

## Paid voucher models

### Model A: voucher is prepaid

Use this when vouchers are sold through a crate, store, NPC, or admin process.

```yaml
vouchers:
  redeem:
    charge-price: false
```

Players are not charged again when redeeming.

### Model B: voucher still charges on redeem

Use this when vouchers are only proof of access, not payment.

```yaml
vouchers:
  redeem:
    charge-price: true
```

The kit price is charged during redemption unless the player has:

```text
crusplayerkits.bypass.price
```

## Safe usage notes

- Use `/kit voucher give` only for trusted staff or automated console systems.
- Keep voucher bypass settings intentional. The default makes vouchers act like direct entitlement items.
- Test redemption with a normal player account before adding vouchers to crates, shops, or rewards.
