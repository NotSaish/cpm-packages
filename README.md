# cpm — Simple Package Manager for Void Linux

A fast, minimal wrapper around `xbps` — built for Void Linux inside Android proot (Termux).

No bloat. No daemon. No fancy output. Just `xbps` with a clean interface.

---

## Installation

### Add the repo

```sh
echo "repository=https://raw.githubusercontent.com/NotSaish/cpm-packages/main/repo/aarch64" \
  > /etc/xbps.d/10-cpm-repo.conf
```

### Install cpm

```sh
xbps-install -S cpm
```

> First time will ask to import the RSA signing key — press `Y` to accept.

---

## Usage

```sh
cpm install <pkg>      # Install package(s)
cpm remove  <pkg>      # Remove package(s) and deps
cpm update             # Sync repos
cpm upgrade            # Upgrade all packages (including cpm itself)
cpm search  <query>    # Search in repos
cpm info    <pkg>      # Show package details
cpm list               # List installed packages
cpm clean              # Remove orphans and cache
cpm size    <pkg>      # Show package size before installing
```

### Flags

```sh
cpm install python3 -y   # Auto confirm
cpm remove nodejs -n    # Auto deny
```

### Short aliases

```sh
cpm i   # install
cpm rm  # remove
cpm up  # upgrade
cpm se  # search
```

---

## Features

### Smart Auto-Sync
Repos sync automatically before install — but only if last sync was over 1 hour ago. Fast installs, no unnecessary network calls.

```sh
cpm update             # Force sync anytime
cpm config set AUTO_SYNC no        # Disable auto sync
cpm config set SYNC_INTERVAL 7200  # Change interval (seconds)
```

### History
```sh
cpm history         # Last 20 actions
cpm history 5       # Last 5 actions
cpm history clear   # Clear log
cpm last            # Last action
```

### Pin Packages
Lock a package from being updated or removed.

```sh
cpm pin python3     # Lock
cpm unpin python3   # Unlock
cpm pinned          # List pinned packages
```

### Snapshots
Save and restore your installed packages list.

```sh
cpm snapshot              # Save as 'default'
cpm snapshot work         # Save with custom name
cpm restore work          # Reinstall from snapshot
cpm snapshots             # List all snapshots
```

### Dependencies
```sh
cpm deps git        # Show package dependencies
```

### Config
```sh
cpm config show               # View current config
cpm config edit               # Edit in $EDITOR
cpm config set AUTO_SYNC no   # Set a value
```

---

## Updating cpm

```sh
cpm upgrade   # cpm updates itself along with system packages
```

---


All cpm data is stored in `~/.cpm/`:

```
~/.cpm/
├── config        # Config file
├── history.log   # Action history
├── pinned        # Pinned packages list
├── last_sync     # Last repo sync timestamp
└── snapshots/    # Saved snapshots
```

---

## License

MIT
