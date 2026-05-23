# registror-backups

Encrypted snapshots of the [Registror](https://github.com/macmariman/registror)
SQLite database. **Do not commit anything here by hand** — the contents are
managed automatically.

## Contents

- `registror-YYYYMMDD-HHMMSS.sqlite3.age` — age-encrypted snapshots. The script
  keeps only the latest 30 and resets git history on every push, so the repo
  stays bounded.
- `.last-hash` — internal marker used by the backup script to skip no-op runs.

## Restore

The private key lives in 1Password (item: "Registror age key"). Restore is done
from the Registror repo:

```
cd ~/Code/Registror
./tools/restore_test.sh
```

The script picks the latest snapshot, asks for the private key, decrypts to a
temp file, and runs integrity checks.

See [docs/backups.md](https://github.com/macmariman/registror/blob/main/docs/backups.md)
in the Registror repo for full details (schedule, encryption, maintenance).
