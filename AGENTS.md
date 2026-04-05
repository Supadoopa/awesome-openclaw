# AGENTS.md

## Repository overview

This is a documentation-only repository: an awesome list of curated OpenClaw, Moltbot, and Clawdbot links. There is no application server, database, package install step, or build pipeline beyond Markdown linting and link checking.

## Important files

- `README.md` is the primary curated list and the safest default target for content edits.
- `README.*.md` files are localized variants. Do not update every translation by default; only touch localized files when the user asks for it or when the task clearly requires translation sync.
- `CONTRIBUTING.md` is the source of truth for contribution formatting, relevance expectations, and commit and PR conventions.
- `.markdownlint.yml` configures Markdown linting.
- `.lychee.toml` configures link checking.
- `.github/workflows/ci.yml` runs Markdown lint and link checking on pull requests, pushes to `main`, manual dispatch, and a weekly schedule.

## Editing rules

- Keep entries directly relevant to the OpenClaw ecosystem.
- Preserve section structure, status-marker legend, footer, and overall document flow unless the task explicitly changes them.
- Keep entries in strict A-Z order within each section.
- Keep each entry on a single bullet line using `- [name](url) - short description.`
- Use status markers only when applicable: `🎖️` for official resources and `💵` for paid services.
- For GitHub repository links, append the social stars badge using `![GitHub stars](https://img.shields.io/github/stars/owner/repo?style=social)`.
- Keep descriptions concise and factual. Prefer what the resource does and why it matters.
- If you add, remove, or rename a section heading in `README.md`, update the Navigation section to match.
- When adding a new resource, include enough evidence in the PR or issue context to justify its relevance to OpenClaw, Moltbot, or Clawdbot.

## Commit and PR conventions

- Follow the semantic prefixes documented in `CONTRIBUTING.md`: `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`, and `ci:`.
- Keep commit messages scoped and specific when possible, for example `docs(readme): add managed hosting resource`.
- PR titles should also use the same semantic style.
- If the task is tied to an issue, link it in the PR body.

## Validation

Run commands from the repo root.

### Markdown lint

- Targeted check for this file: `markdownlint-cli2 "AGENTS.md"`
- Repo-wide check: `markdownlint-cli2 "**/*.md"`

`markdownlint-cli2` uses `.markdownlint.yml`. Root-level Markdown files should be kept lint-clean.

### Link check

- Targeted check for this file: `lychee --config .lychee.toml --no-progress "AGENTS.md"`
- Repo-wide check: `lychee --config .lychee.toml --no-progress "./**/*.md"`

`lychee` uses `.lychee.toml`. Setting `GITHUB_TOKEN` reduces GitHub rate-limit noise. Some external sites may intermittently fail from the cloud VM; distinguish new failures from pre-existing or transient network issues before treating them as regressions.

## Expected command results

- `markdownlint-cli2` exits with code `0` when lint passes and `1` when lint errors are found.
- `lychee` exits with code `0` when links pass and `2` when link errors are found.

## Gotchas

- There is no `docs/` directory in the current repository layout; prefer instructions that reference the root README files and config files that actually exist.
- Do not add package-manager setup or application runtime instructions unless the repository structure changes in the future.
- `markdownlint-cli2` is available globally, and `lychee` is installed as a standalone binary in the cloud environment.
