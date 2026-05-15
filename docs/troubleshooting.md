# Troubleshooting

Use this page to diagnose common CrusPlayerKits setup and runtime issues.

## Plugin does not start

| Check | Action |
|---|---|
| Java version | Use Java 21 or newer. |
| Server platform | Use Paper, Purpur, or Folia. Spigot/Bukkit compatibility is not guaranteed. |
| Console errors | Read the first error, not only the last line. Missing dependencies, invalid config, or storage errors usually appear early. |
| Plugin file | Confirm the JAR is in `plugins/` and the server was fully restarted. |

## `/kit` does not open

| Cause | Fix |
|---|---|
| Player lacks permission | Give `crusplayerkits.use`. |
| Command conflict | Check whether another plugin also registers `/kit` or `/kits`. Use plugin command aliases or remove the conflict. |
| Plugin not loaded | Check `/plugins` and console startup logs. |
| GUI config issue | Check `menu.size`, category menu size, and material names. |

## Player cannot claim a kit

Run:

```text
/kit info <kit>
```

Then check:

| Cause | Fix |
|---|---|
| Missing kit permission | Give `crusplayerkits.kit.<kit>`. |
| Cooldown active | Wait, reset with `/kit reset <player> <kit>`, or give `crusplayerkits.bypass.cooldown`. |
| One-shot already claimed | Reset with `/kit reset <player> <kit>` or give `crusplayerkits.bypass.oneshot`. |
| Paid kit economy unavailable | Install Vault and an economy provider, or set the kit price to `free`. |
| Not enough money | Adjust economy balance or kit price. |
| Inventory full | Enable `claim.drop-if-full` or ask the player to clear space. |
| Empty kit | Edit or recreate the kit with items or command rewards. |

## Paid kits do not work

| Cause | Fix |
|---|---|
| Vault is missing | Install Vault and restart. |
| Economy provider is missing | Install a Vault-compatible economy plugin. |
| Economy disabled | Set `economy.enabled: true`. |
| Price is not set | Use `/kit price <kit> <amount>`. |
| Player bypasses price | Remove `crusplayerkits.bypass.price` or `crusplayerkits.admin`. |

## Vouchers do not redeem

| Cause | Fix |
|---|---|
| Vouchers disabled | Set `vouchers.enabled: true`. |
| Player right-clicked with offhand | Redeem from the main hand. |
| Kit was deleted | Recreate the kit or issue new vouchers. |
| Redemption charges price | Check `vouchers.redeem.charge-price`. |
| Inventory full | Clear inventory space or enable `claim.drop-if-full`. |

If redemption fails, CrusPlayerKits restores the voucher stack when possible.

## Categories do not show correctly

| Cause | Fix |
|---|---|
| Only one category exists | Category landing page is used when categories are enabled and multiple categories exist. |
| Empty category hidden | Set `categories.show-empty: true` or add visible kits. |
| Category permission missing | Give the configured category permission. |
| Kit in wrong category | Use `/kit category <kit> <category>`. |
| Invalid material | Use a valid Bukkit material or supported head material spec. |

## First-join starter kits do not claim

Check the `starter` category:

```yaml
categories:
  items:
    starter:
      auto-claim:
        first-join: true
```

Then verify:

| Cause | Fix |
|---|---|
| Player is not new | If `only-new-players` is true, existing players will not be processed as new. |
| Category already processed | Reset with `/kit reset <player> all`. |
| Inventory full | Clear inventory or configure `claim.drop-if-full`. |
| Permissions are respected | If enabled, the player must have category and/or kit permissions. |
| Storage failing | Check player data save errors in console. |

## Import shows skipped or failed kits

| Result | Meaning | Fix |
|---|---|---|
| Skipped | Kit already exists and `--overwrite` was not used. | Add `--overwrite` or rename the imported kit. |
| Failed | The importer could not create a usable kit. | Review console warnings and recreate unsupported items manually. |
| File not found | The importer path is wrong. | Provide the full file path. |

## SQL storage errors

| Cause | Fix |
|---|---|
| Wrong MySQL credentials | Check host, port, database, username, and password. |
| Database missing | Create the database before starting the server. |
| Network blocked | Check firewall and hosting panel database access. |
| SSL mismatch | Adjust `storage.mysql.use-ssl` and JDBC parameters. |
| Table permission missing | Grant the database user permission to create and update tables. |

If SQL fails, CrusPlayerKits attempts YAML fallback. Treat fallback as temporary and fix the database issue.

## Safe recovery steps

1. Stop the server.
2. Back up `plugins/CrusPlayerKits/`.
3. Fix the relevant configuration file.
4. Start the server.
5. Check console startup logs.
6. Test with a normal player account.

For config-only changes, `/kit reload` is usually enough. For dependency, JAR, Java, or storage driver changes, restart the server.
