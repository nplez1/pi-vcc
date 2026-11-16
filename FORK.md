# pi-vcc (pi-config fork of `sting8k/pi-vcc`)

Local fork, installed as `plugins/pi-vcc` in `~/.pi/agent/settings.json`
(resolved through `~/.pi/agent/plugins`, a symlink to the pi-config repository's
`plugins/`). Upstream is `sting8k/pi-vcc`, MIT, version **0.11.2**.

## Why a fork

pi-config's convention: every plugin it ships is a fork under `nplez1/` so a
local change cannot be silently overwritten by `pi update --extensions`, and so
the change is written down where the installer and the next reader look for it.
A fork also lets the submodule pin an exact commit instead of tracking an npm
release — the plugin overrides `/compact` and automatic compaction, so the
version that loads has to be the version that was tested against this host.

Upstream history is preserved (the fork is a plain GitHub fork of
`sting8k/pi-vcc`, no squash, no re-init), so `git merge upstream/master` stays
available — unlike the squashed forks of the other plugins.

## Divergence from upstream 0.11.2

None yet. `master` is upstream `master` exactly (`git diff upstream/master` is
empty at the time of forking); the only commit this fork adds is this file.

## Related notes for pi-config

- The config file `~/.pi/agent/pi-vcc-config.json` is **machine-owned**. The
  extension writes it with its defaults on first load and fills in keys added by
  a later release; pi-config tracks no seed and no symlink for it, so a machine
  keeps its own `overrideDefaultCompaction` / `skipForProviders` /
  `trackCommands` choices across installs.
- No dependencies to install: `typebox` and `@earendil-works/pi-*` are peer
  dependencies supplied by the host's extension loader. `bun.lock` and the
  `devDependencies` are upstream's contributor toolchain, not runtime.
- Pi-Bolt compiles installed extensions into its executable. After changing this
  fork, re-run `install.sh` (or `pi-bolt compile`) to pick the change up.

## Re-syncing with upstream

```sh
git remote add upstream https://github.com/sting8k/pi-vcc.git
git fetch upstream && git merge upstream/master
```

Nothing else is intentionally changed. Compare `git diff upstream/master` — only
this file should appear.
