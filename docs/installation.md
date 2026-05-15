# Installation guide

This guide covers a clean installation of CrusPlayerKits on a modern Paper, Purpur, or Folia server.

## Requirements

| Component | Required | Notes |
|---|---:|---|
| Java 21+ | Yes | The plugin is built for Java 21. |
| Paper, Purpur, or Folia | Yes | These are the intended server platforms. |
| PlaceholderAPI | No | Required only if you want `%crusplayerkits_*%` placeholders. |
| Vault | No | Required for paid kits. |
| Economy plugin | No | Required together with Vault for paid kits. Examples: EssentialsX Economy or another Vault-compatible economy provider. |

> [!WARNING]
> Avoid using `/reload` or plugin-manager hot reloads on production servers. Fully restart the server when installing, updating, or changing storage drivers.

## Install the plugin

1. Stop the server.
2. Place `CrusPlayerKits.jar` inside the server `plugins/` folder.
3. Install optional dependencies if needed:
   - `PlaceholderAPI` for placeholders.
   - `Vault` plus a Vault-compatible economy plugin for paid kits.
4. Start the server.
5. Confirm that these files are generated:

```text
plugins/CrusPlayerKits/config.yml
plugins/CrusPlayerKits/messages.yml
plugins/CrusPlayerKits/kits.yml
```

Player data is generated after players begin claiming kits.

## Verify the installation

Run these commands in game:

```text
/kit
/kit list
/kit help
```

Expected result:

- `/kit` opens the category or kit GUI.
- `/kit list` lists existing kits if any are configured.
- `/kit help` shows the command list available to your permissions.

## Optional: install PlaceholderAPI support

1. Install PlaceholderAPI.
2. Restart the server.
3. Use the placeholders listed in [PlaceholderAPI](placeholders.md).

The placeholder expansion registers under this identifier:

```text
crusplayerkits
```

## Optional: install economy support

1. Install Vault.
2. Install a Vault-compatible economy plugin.
3. Enable economy in `config.yml`:

```yaml
economy:
  enabled: true
  require-vault: false
```

4. Set a price on a kit:

```text
/kit price warrior 5000
```

See [Economy prices](economy-prices.md) for the complete behavior.

## Optional: configure SQL storage

CrusPlayerKits stores kit definitions in `kits.yml`. SQL storage is used for player claim data: cooldowns, one-time claims, and processed category auto-claims.

Use [Storage setup](storage-setup.md) before enabling SQLite or MySQL.

## Update checklist

1. Stop the server.
2. Back up `plugins/CrusPlayerKits/`.
3. Replace the plugin JAR.
4. Start the server.
5. Check console for warnings.
6. Run:

```text
/kit reload
/kit list
```

`/kit reload` reloads configuration, messages, categories, kits, economy state, and player data. It is not a replacement for a full server restart after installing a new JAR.
