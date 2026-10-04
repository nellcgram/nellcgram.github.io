# How I built this site

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

## What each check caught

These examples come from the pull requests that built this pipeline.

- **Strict build:** nothing so far. `mkdocs build --strict` has passed on every pull request, so it hasn't caught a real problem yet. It exists to fail on a broken navigation entry or a Markdown warning.
- **markdownlint:** when I added it, it found 11 problems in existing pages. They were trailing spaces, a malformed table, a missing blank line before a heading, and a bare email address. Later it flagged a compact table separator row and another missing blank line in newer pages.
- **Link check:** on one pull request, lychee failed three times on a link to my `docs-assistant` repository, which returned a 503 error from GitHub. The link was fine. The check passed a few minutes later with no change to the link. A failed link check is a reason to look, not proof that a link broke.
- **Vale:** the first run showed three problems in my own setup. Google's rules for em dashes and ordinal numbers ran as errors, and they would have blocked any pull request that touched those lines. One rule message printed an empty term. The heading rule flagged the pronoun "I." It also found real writing issues: 7 title-case headings and 11 passive-voice sentences. I fixed the setup problems and exempted my portfolio pieces from Google's rules, so their published wording stays. Vale now reports 2 alerts across the site. The [NellStyle rules](https://github.com/nellcgram/nellcgram.github.io/blob/main/.vale/styles/NellStyle/README.md) list each check and its known false positives.
- **Preview and deploy:** the original deploy command, `mkdocs gh-deploy --force`, rewrote the whole `gh-pages` branch and deleted every open preview, so a preview link returned a 404. Previews also never cleaned up, because the workflow didn't listen for the pull request closing. [Pull request 11](https://github.com/nellcgram/nellcgram.github.io/pull/11) fixed both. After it merged, a preview survived a deploy to `main`, which the old command would have deleted.

## Deployment

I first deployed with `mkdocs gh-deploy` from the command line. I then moved to a GitHub Actions workflow that deploys on every push to `main`, which removed the manual step.

The workflow builds the site with `mkdocs build --strict` and publishes it to the `gh-pages` branch, which GitHub Pages serves. It keeps the `pr-preview/` folder, so open previews survive a deploy.

Source: [.github/workflows/](https://github.com/nellcgram/nellcgram.github.io/tree/main/.github/workflows)

## Repository

Source code: [github.com/nellcgram/nellcgram.github.io](https://github.com/nellcgram/nellcgram.github.io)

See [CONTRIBUTING.md](https://github.com/nellcgram/nellcgram.github.io/blob/main/CONTRIBUTING.md) for the contributing guide.
