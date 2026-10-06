# AGENTS.md

## Project context

Training repository for collaborative GitHub workflows (issues, pull requests, reviews, Conventional Commits, ADRs). The stack runs ~15 Docker services across two servers behind a reverse proxy. All infrastructure changes go through a reviewed pull request — no direct edits in production.

## Verification commands

Check that your branch is up to date with main before opening a PR:

```bash
git fetch origin
git log origin/main..HEAD --oneline
```

Verify your commit messages follow Conventional Commits before pushing:

```bash
git log --oneline
```

## Conventions

- **Branches:** `<type>/<short-description>` — e.g. `feat/user-auth`, `docs/4-documentation`, `fix/vpn-firewall`
- **Commits:** [Conventional Commits](https://www.conventionalcommits.org/) — `type(scope): description` in lowercase, imperative mood
- **PR title:** same format as the commit message
- **PR description:** fill every section of the template; include `Closes #<issue-number>` when applicable
- **Merge strategy:** Squash and merge only — keeps main history linear
- **Review comments:** follow [Conventional Comments](https://conventionalcomments.org/) — `label (decoration): subject`

## Forbidden

- Do not push directly to `main` — all changes go through a pull request
- Do not merge your own PR without at least one approval
- Do not use `--force` or `--no-verify` without explicit team agreement
- Do not commit secrets, credentials, or `.env` files
- Do not skip the PR description template
