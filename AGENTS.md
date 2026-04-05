# AGENTS.md

## Cursor Cloud specific instructions

This is a documentation-only repository (an "awesome list" of curated links).
There is no application server, database, or build step.
The product is a collection of Markdown files.

## Scope and expectations

- Default work type: edit Markdown files and keep formatting consistent.
- Prefer small, focused commits for each logical content change.
- Do not add app/runtime setup instructions unless specifically requested.
- Validate only the files or sections you touched when possible.

### Services & tools

| Tool | Purpose | Command |
| --- | --- | --- |
| `markdownlint-cli2` | Lint Markdown formatting | `markdownlint-cli2 "**/*.md"` |
| `lychee` | Check for dead links | `lychee --config .lychee.toml --no-progress './**/*.md'` |

## Standard workflow for agents

1. Make requested Markdown updates.
2. Run lint checks.
3. Run link checks when links were added or changed.
4. Summarize exact files changed and command outputs.

### Lint

Run from the repo root:

```sh
markdownlint-cli2 "**/*.md"
```

Config lives in `.markdownlint.yml`.
Root-level `*.md` files should pass cleanly.
`docs/` contains pre-existing violations.

### Link check

```sh
lychee --config .lychee.toml --no-progress './**/*.md'
```

Config lives in `.lychee.toml`.
Setting a `GITHUB_TOKEN` env var reduces GitHub rate-limit errors.
Some external URLs may be unreachable from the cloud VM (network errors, 503s).
Treat these as external failures unless the edited link is clearly malformed.

### CI reference

The GitHub Actions workflow (`.github/workflows/ci.yml`) runs both tools on:

- Every push to `main`
- Every pull request targeting `main`
- A weekly scheduled run

### Gotchas

- `lychee` exit code `2` means link errors were found. Exit code `0` means all links are valid.
- `markdownlint-cli2` exit code `1` means lint errors were found.
- Existing lint errors are in `docs/`; root-level README files should be clean.
- There is no `package.json` or lockfile in this repo.
- `markdownlint-cli2` is installed globally via npm; `lychee` is a standalone binary.

## Definition of done for typical docs edits

- Requested content change is present and accurate.
- Markdown lint passes for the relevant files.
- Link checks are run when URLs were touched.
- Final summary includes what changed and evidence from command output.
