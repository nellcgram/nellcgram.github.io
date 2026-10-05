# How I build this site

I build this site with [MkDocs](https://www.mkdocs.org/) and host it on
[GitHub Pages](https://pages.github.com/). The source files live in a public
GitHub repository. Every change goes through a pull request, automated checks,
and a preview before it reaches the live site.

## Toolchain

| Tool | Purpose |
| --- | --- |
| MkDocs | Static site generator that converts Markdown files to HTML |
| GitHub | Version control and remote repository hosting |
| GitHub Pages | Free static site hosting, deployed with GitHub Actions |
| GitHub Actions | Runs the checks on every pull request and deploys the site when a change merges |
| markdownlint | Checks Markdown formatting, including heading structure, image alt text, and blank lines |
| lychee | Checks that internal and external links work |
| Vale | Checks prose against the Google developer documentation style guide and my own rules |
| pr-preview-action | Publishes a rendered preview of each pull request |
| VS Code | Local file editing |
| Claude Code | AI pair-writing assistant used inside VS Code for drafting and revising content, and for building/testing the AI skills documented elsewhere on this site |
| Terminal | Running MkDocs commands and Git operations |

## Workflow

1. Create a branch and edit `.md` files locally in VS Code, using Claude Code for editing assistance and content review.
2. Preview the changes locally with `mkdocs serve`.
3. Commit the changes and push the branch to GitHub.
4. Open a pull request into `main`. Continuous integration (CI) starts automatically.
5. CI runs five jobs: a strict MkDocs build, markdownlint, a link check, Vale prose linting, and a preview deployment.
6. Open the preview link that a bot posts on the pull request, and read the rendered pages.
7. Merge when the checks pass. The deploy workflow publishes the site to GitHub Pages and removes the preview.

## Deployment

I first deployed with `mkdocs gh-deploy` from the command line. I then moved to a GitHub Actions workflow that deploys on every push to `main`, which removed the manual step.

The workflow builds the site with `mkdocs build --strict` and publishes it to the `gh-pages` branch, which GitHub Pages serves. It keeps the `pr-preview/` folder, so open previews survive a deploy.

Source: [.github/workflows/](https://github.com/nellcgram/nellcgram.github.io/tree/main/.github/workflows)

## Repository

Source code: [github.com/nellcgram/nellcgram.github.io](https://github.com/nellcgram/nellcgram.github.io)

See [CONTRIBUTING.md](https://github.com/nellcgram/nellcgram.github.io/blob/main/CONTRIBUTING.md) for the contributing guide.
