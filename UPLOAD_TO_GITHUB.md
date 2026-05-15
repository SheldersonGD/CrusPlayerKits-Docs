# Upload this documentation to GitHub

Target repository:

```text
git@github.com:SheldersonGD/CrusPlayerKits-Docs.git
```

This guide assumes you have Git installed and your SSH key already connected to GitHub.

## Option A — Fresh clone, then copy the files

Clone the repository:

```bash
git clone git@github.com:SheldersonGD/CrusPlayerKits-Docs.git
cd CrusPlayerKits-Docs
```

Copy the documentation files from the generated package into this folder.

Your final folder should look like this:

```text
CrusPlayerKits-Docs/
├─ README.md
├─ UPLOAD_TO_GITHUB.md
├─ SECURITY.md
├─ .gitignore
└─ docs/
   ├─ index.md
   ├─ installation.md
   ├─ commands.md
   ├─ permissions.md
   ├─ configuration.md
   ├─ categories.md
   ├─ vouchers.md
   ├─ economy-prices.md
   ├─ storage-setup.md
   ├─ importers.md
   ├─ troubleshooting.md
   └─ placeholders.md
```

Check the changed files:

```bash
git status
```

Commit and push:

```bash
git add README.md UPLOAD_TO_GITHUB.md SECURITY.md .gitignore docs/
git commit -m "Add CrusPlayerKits documentation"
git push origin main
```

If your default branch is `master`, use:

```bash
git push origin master
```

## Option B — Existing local repository

Open your existing docs repository folder:

```bash
cd CrusPlayerKits-Docs
```

Pull the latest remote changes:

```bash
git pull
```

Copy the generated documentation files into the repository, replacing old docs if needed.

Commit and push:

```bash
git add README.md UPLOAD_TO_GITHUB.md SECURITY.md .gitignore docs/
git commit -m "Update CrusPlayerKits documentation"
git push
```

## If Git says the branch name is wrong

Check the branch:

```bash
git branch
```

Push to the branch that has the `*` mark:

```bash
git push origin <branch-name>
```

## If SSH does not work

Test SSH access:

```bash
ssh -T git@github.com
```

If GitHub rejects the key, add your public SSH key to GitHub account settings and retry.

## Do not upload these files

Before pushing, check that none of these are staged:

```text
plugins/CrusPlayerKits/player_data.yml
plugins/CrusPlayerKits/player_data.db
plugins/CrusPlayerKits/edit_backups.yml
*.sql
*.db
*.jar
.env
```

This docs package already includes a `.gitignore` that blocks common sensitive/runtime files.
