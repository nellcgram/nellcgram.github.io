# Contributing

This is a personal portfolio site, but it follows a docs-as-code workflow:
content changes go through a pull request, automated checks, and a
reviewable preview before merging to `main`.

## Local development

```bash
pip install -r requirements.txt
mkdocs serve
```

## Workflow

1. Create a branch and edit files under `docs/`.
2. Open a pull request into `main`.
3. CI runs automatically on the PR (see below). Fix any failures.
4. Review the PR preview deployment (link posted to the PR by the preview
   bot) to see the rendered change before merging.
5. Merge to `main` — the deploy workflow publishes the site to GitHub
   Pages automatically.

## What CI checks on every PR

| Check | Tool | Fails the build on |
| --- | --- | --- |
| Build | `mkdocs build --strict` | Broken nav entries, bad Markdown, MkDocs warnings |
| Style/format | [markdownlint-cli2](https://github.com/DavidAnson/markdownlint-cli2) | Heading structure, missing image alt text, formatting issues (`.markdownlint-cli2.jsonc`) |
| Links | [lychee](https://github.com/lycheeverse/lychee) | Dead internal or external links (`.lychee.toml`) |
| Preview | [pr-preview-action](https://github.com/rossjrw/pr-preview-action) | N/A — deploys a rendered preview of the PR to `gh-pages/pr-preview/pr-<number>/` |

Run the same checks locally before pushing:

```bash
mkdocs build --strict
npx markdownlint-cli2 "docs/**/*.md"
```

## Versioning

This site has a single live version — there's no versioned docs history to
switch between, so there's no version-switcher (e.g. `mike`) in the build.
