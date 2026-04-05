# AGENTS.md

## Cursor Cloud specific instructions

This is a **documentation-only** repository (an "awesome list" of curated links). There is no application server, database, or build step. The "product" is a collection of Markdown files.

### Services & tools

| Tool | Purpose | Command |
| --- | --- | --- |
| `markdownlint-cli2` | Lint Markdown formatting | `markdownlint-cli2 "**/*.md"` |
| `lychee` | Check for dead links | `lychee --config .lychee.toml --no-progress './**/*.md'` |

### Lint

Run from the repo root:

```sh
markdownlint-cli2 "**/*.md"
```

Config lives in `.markdownlint.yml`. The root-level `*.md` files should pass cleanly; `docs/` files have pre-existing violations.

### Link check

```sh
lychee --config .lychee.toml --no-progress './**/*.md'
```

Config lives in `.lychee.toml`. Setting a `GITHUB_TOKEN` env var reduces GitHub rate-limit errors. Some external URLs may be unreachable from the cloud VM (network errors, 503s); these are pre-existing broken links, not environment issues.

### CI reference

The GitHub Actions workflow (`.github/workflows/ci.yml`) runs both tools above on every push and PR to `main`. It also runs weekly on a schedule.

### Gotchas

- `lychee` exit code 2 means link errors were found (pre-existing). Exit code 0 means all links are valid.
- `markdownlint-cli2` exit code 1 means lint errors were found. All lint errors in the current repo are in `docs/` — the root-level README files pass cleanly.
- There is no `package.json` or lockfile in this repo. `markdownlint-cli2` is installed globally via npm, and `lychee` is a standalone binary.
