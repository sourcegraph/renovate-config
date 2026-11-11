# AGENTS.md

## Overview

This repo holds a shared [Renovate](https://docs.renovatebot.com/) configuration
preset reused across Sourcegraph repositories. The published preset is
`default.json`; other repos extend it (e.g. `"extends": ["github>sourcegraph/renovate-config"]`).

There is no application code, build step, or test suite — changes are config edits.

## Layout

- `default.json` — the shared Renovate preset that other repositories extend.
- `renovate.json` — this repo's own Renovate config (extends the local preset).
- `prettier.config.js` / `.prettierignore` — formatting config (extends `@sourcegraph/prettierrc`).
- `.editorconfig` — 2-space indent, LF line endings, final newline, no trailing whitespace.

## Setup

Node tooling is managed with Yarn (`yarn.lock` is committed). Install dev
dependencies before formatting:

```bash
yarn install
```

## Conventions

- JSON config is formatted with Prettier; `package.json` and `package-lock.json`
  are excluded via `.prettierignore`.

```bash
yarn prettier --write '**/*.{json,js,md}'
```

- Validate JSON files are well-formed after editing, e.g.:

```bash
node -e "require('./default.json'); require('./renovate.json')"
```

- Renovate preset semantics follow the
  [Renovate configuration schema](https://docs.renovatebot.com/renovate-schema.json)
  referenced by the `$schema` field. Keep new `packageRules` consistent with the
  existing grouping/labeling patterns in `default.json`.
