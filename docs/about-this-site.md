# About This Site

This portfolio is built with [MkDocs](https://www.mkdocs.org/) and hosted on
[GitHub Pages](https://pages.github.com/). The source files are version-controlled
in a public GitHub repository.

## Toolchain

| Tool | Purpose |
| --- | --- |
| MkDocs | Static site generator; converts Markdown files to HTML |
| GitHub | Version control and remote repository hosting |
| GitHub Pages | Free static site hosting, deployed via GitHub Actions |
| Visual Studio Code | Local file editing |
| Claude Code | AI pair-writing assistant used inside VS Code for drafting and revising content, and for building/testing the AI skills documented elsewhere on this site |
| Terminal | Running MkDocs commands and Git operations |

## Workflow

1. Draft or revise .md files locally in VS Code, using Claude Code for editing assistance and content review
2. Preview changes locally with `mkdocs serve`
3. Stage and commit changes via Git
4. Push to `main` — GitHub Actions deploys automatically

## Deployment

Initially deployed using `mkdocs gh-deploy` from the command line. Migrated to a
GitHub Actions workflow to automate deployment on every push to `main`, eliminating
the manual deploy step.

The Actions workflow builds the site and publishes to GitHub Pages automatically
whenever changes are merged.

Source: [.github/workflows/](https://github.com/nellcgram/nellcgram.github.io/tree/main/.github/workflows)

## Repository

Source code: [github.com/nellcgram/nellcgram.github.io](https://github.com/nellcgram/nellcgram.github.io)
