# CodeVault

Private Obsidian vault that surfaces every project under `~/workspace/`.

## How it works

- **Provisioning** — Nix (`dots/nixos-config/modules/workspace.mod.nix`) clones
  the owned-upstream manifest into `~/workspace/`, then runs the script below.
  It never clones third-party projects.
- **Vault surface** — [`bin/relink`](bin/relink) symlinks every subdirectory of
  `~/workspace/` into `projects/` (idempotent; prunes stale links). So anything
  you drop into `~/workspace/` by hand shows up here too, no config change.

## Regenerate the links

```sh
bin/relink              # uses ~/workspace
bin/relink /path/to/ws  # or an explicit workspace root
```

`projects/` is git-ignored: the symlinks are machine-local and regenerated,
never committed. Notes and `.obsidian/` config are tracked normally.
