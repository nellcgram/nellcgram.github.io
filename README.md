# Portfolio site

Source files for [nellcgram.github.io](https://nellcgram.github.io), a technical writing portfolio built with MkDocs and hosted on GitHub Pages.

## Tech stack

- MkDocs builds the site from the Markdown files in `docs/`.
- GitHub Actions runs the checks and deploys the site.
- markdownlint, lychee, and Vale check formatting, links, and prose style.

## Local development

```bash
pip install -r requirements.txt
mkdocs serve
```

## How a change reaches the site

1. Create a branch and edit files under `docs/`.
2. Open a pull request into `main`.
3. CI runs a strict build, markdownlint, a link check, and Vale prose linting. It also publishes a preview of the pull request.
4. Review the preview, then merge when the checks pass.
5. The deploy workflow publishes the site to GitHub Pages and removes the preview.

For the toolchain and deployment details, see [How I build this site](https://nellcgram.github.io/how-I-build-this-site.html).

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for the PR workflow, CI checks, and local
validation commands.
