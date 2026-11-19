# stack-nudge extensions marketplace

The public catalogue of [stack-nudge](https://github.com/StackOneHQ/stack-nudge) extensions.
Each merge that changes an extension publishes a release here, and stack-nudge installs and
updates extensions from it, separately from releases of the app itself.

| Extension | What it does |
|---|---|
| `away` | Notices when you walk away from the Mac with your phone, so stack-nudge can lock the screen. A service, at `trusted` |
| `derby` | The Token Derby, a shared horse race scored on tokens produced |
| `pylon` | Customer issues in your Pylon workspace that are waiting on a response, with a banner before a first-response SLA runs out |
| `system` | CPU, memory and disk at a glance |

Made from
[StackOneHQ/stack-nudge-extensions-template](https://github.com/StackOneHQ/stack-nudge-extensions-template),
like [StackOneHQ/stack-nudge-internal-marketplace](https://github.com/StackOneHQ/stack-nudge-internal-marketplace),
so all three are laid out, checked and released the same way.

## How stack-nudge reads it

This is stack-nudge's own catalogue: read first, always, and one of the catalogues the app lets
grant tiers above `view`, so `extensions/tiers.json` here decides them. Until the app version
that reads it from here is the one everybody runs, stack-nudge's own releases carry a copy of
this repo's latest index and packages, so older copies of the app keep getting updates too.

The extensions moved here from `extensions/` in StackOneHQ/stack-nudge with their history.
References like `StackOneHQ/stack-nudge#245` in older commits are pull requests there.

## Releases

Every merge to `main` that changes an extension publishes `extensions-<run>`, marked latest,
with every package, its `.sha256` file and `extensions-index.json`. The notes list each
extension with its version and tier, and what's new or updated since the release before.
stack-nudge offers an update when an installed extension's version differs from the index, so
every change to an extension bumps its version, and CI fails one that doesn't.

## Layout

- `extensions/`: one directory per extension, plus `tiers.json`. Only this is packaged.
- `scripts/`: `check.sh` runs every check. `package-extensions.sh`, `test-extensions.sh` and
  `check-extension-versions.sh` are stack-nudge's, `check-workflows.mjs` agent-control's,
  `release-notes.mjs` the template's.
- `vendor/`: stack-nudge's manifest enum, which the packager reads for the known capabilities.
- `.github/workflows/`: `ci.yml` checks the PR title and validates, tests and version-checks the
  extensions on every pull request, `release.yaml` publishes on every merge that changes an
  extension.
- `.claude/skills/`: Claude Code skills for building (`new-extension`), trying
  (`try-extension`) and reviewing (`review-extension`) an extension.

## What you need

- python3, for the extensions and their tests, and the Xcode Command Line Tools for `away`
- Node 22.23.4 and pnpm 11.17.0, for the lint, the script specs and the git hooks
- shellcheck and actionlint if you want those checks to run; they're skipped otherwise

```bash
pnpm install   # also turns on the git hooks in .githooks/
pnpm check     # scripts/check.sh: every part, one line each
```

## Where the docs are

- `CONTRIBUTING.md`: branches, commits, adding or changing an extension and what review looks for
- `AGENTS.md`: the rules for agents (`CLAUDE.md` links to it)
- `SECURITY.md` and `PRIVACY.md`: reporting a problem, and what each extension reads and sends
- stack-nudge's [extension docs](https://github.com/StackOneHQ/stack-nudge/blob/main/docs/extensions.md),
  the spec for the manifest and the document an extension prints
