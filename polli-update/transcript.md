# polli update — isolated installation demo

Live demonstration of the `polli update` command from this PR, run against an
isolated npm prefix (`NPM_CONFIG_PREFIX=/tmp/polli-demo`), so the system-wide
installation is never touched.

Setup: a test build of this PR (version labeled `0.0.1`) was installed globally
into the isolated prefix, then updated in place.

```console
$ npm install -g ./pollinations-cli-0.0.1.tgz        # test build into the isolated prefix
$ /tmp/polli-demo/bin/polli --version
0.0.1 — Mostly harmless.                             # (test build label)

$ /tmp/polli-demo/bin/polli update
Updating @pollinations/cli (v0.0.1 → v0.1.15)...     # printInfo (stderr)

changed 18 packages in 3s                            # npm itself, delegated to

previous: 0.0.1                                      # printResult (stdout)
version: 0.1.15
installType: global
updated: true

$ /tmp/polli-demo/bin/polli --version
0.1.15 — Mostly harmless.                            # confirmed running the new version
```

What this demonstrates:

1. `polli update` detects a **global** npm install from the on-disk location
   (`npm root -g` inside the isolated prefix).
2. It asks npm for the latest published version and installs exactly that
   (`npm install -g @pollinations/cli@0.1.15`) — explicit, user-requested,
   no sudo, no silent updates.
3. The result is reported through the CLI's existing machine-readable output
   conventions (`printResult`), so `--json` consumers stay supported.
