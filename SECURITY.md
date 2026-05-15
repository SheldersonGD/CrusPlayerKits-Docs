# Security notes

This repository is intended for public-safe documentation.

## Do not commit private data

Never commit:

- Production `player_data.yml` files.
- SQLite databases such as `player_data.db`.
- MySQL dumps or backup files.
- Real database usernames, passwords, hosts, or ports.
- Private server IP addresses or staff-only notes.
- Paid plugin JAR files unless distribution is intentionally allowed.
- License keys, store tokens, API keys, or `.env` files.

## Recommended workflow

Use example values in documentation:

```yaml
username: "minecraft_user"
password: "replace-with-a-secure-password"
```

Keep production configuration outside the documentation repository.

## Reporting security issues

If you maintain a private support channel, direct users there for sensitive reports. Public issues should not include secrets, server addresses, database credentials, or exploitable production details.
