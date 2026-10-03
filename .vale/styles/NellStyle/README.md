# NellStyle: custom Vale rules

These rules run on top of the [Google developer documentation style guide](https://developers.google.com/style) package. `.vale.ini` loads both, so a page gets checked against Google's rules and these.

Severity decides what blocks a pull request. Only `error` rules fail CI. `warning` and `suggestion` alerts show up as annotations and never block a merge.

## Rules

| Rule | File | Severity | What it flags |
| --- | --- | --- | --- |
| Heading case | `HeadingCase.yml` | warning | Headings that aren't sentence case (the pronoun "I" and listed proper nouns are allowed) |
| Product names | `ProductNames.yml` | error | Wrong capitalization of GitHub, MkDocs, Markdown, Claude Code, Visual Studio Code |
| Editor name | `EditorName.yml` | warning | A page that uses both "VS Code" and "Visual Studio Code" |
| Filler words | `FillerWords.yml` | warning | simply, just, easy, easily, basically, obviously, actually, clearly |
| Inflated words | `InflatedWords.yml` | warning | leverage, utilize, "in order to" |
| Passive voice | Google's `Google.Passive` | suggestion | Passive constructions such as "was checked" |
| Sentence length | `SentenceLength.yml` | suggestion | Sentences over 30 words |
| Acronyms | `Acronyms.yml` | suggestion | Three to five letter acronyms not spelled out on first use |
| Placeholders | `Placeholders.yml` | error | TODO, TBD, FIXME, lorem ipsum, XXX |
| UI terms | `UiTerms.yml` | warning | "click on", "log in", "login" |

## Results on this site's pages

### First run (PR #13)

These counts come from the Vale job on PR #13, the first run, after the config fixes below and before any page was edited or exempted. Later changes to the pages and to `.vale.ini` made them out of date, so the next section shows the current state.

| Rule | Alerts | What they were |
| --- | --- | --- |
| Heading case | 7 | "How This Site is Built", "Contact Information", "Release Notes", "eReader App Monthly Updates", "Help Center Article", "Internal Knowledge Base Article", and the case study title. All are real title-case headings. |
| Product names | 0 | |
| Editor name | 2 | `how-this-site-is-built.md` uses "Visual Studio Code" once and "VS Code" twice. |
| Filler words | 0 | |
| Inflated words | 1 | "leverage" in `release-notes.md`. |
| Passive voice (`Google.Passive`) | 11 | Includes "was checked", "were created", and the headline "is Built". |
| Sentence length | 2 | A long bullet in `release-notes.md` and a long paragraph in `docs-assistant.md`. |
| Acronyms | 0 | |
| Placeholders | 0 | |
| UI terms | 0 | |

False positives found in that run and fixed:

- **Heading case flagged "What I built" and "What I learned".** Vale treated the pronoun "I" as a capitalization error. "I" is now in the `exceptions` list, along with "Story Board".
- **The editor-name message printed an empty term.** The rule used a placeholder that this rule type does not fill. The message is now plain text.
- **Google's own `EmDash` and `Ordinal` rules are errors.** They flagged spaced em dashes and "7th", and would have failed any PR that edited those lines. `.vale.ini` now sets both to warning.

False positives from that run that exemptions now hide:

- **"is unresolved" in `docs-assistant.md`** was flagged as passive voice, but "unresolved" is an adjective.
- **`Google.WordListCase`, `Google.Colons`, `Google.Will` and `Google.Contractions`** produced many warnings on the portfolio pages' deliberate wording. They're Google rules, not NellStyle rules, and none blocks a merge.

### Current state (PR #14)

After the exemptions in `.vale.ini` and edits to `how-this-site-is-built.md`, the Vale job on PR #14 (Oct 3, 2026) reported 2 alerts across all of `docs/`. Both are in `docs/index.md` and neither blocks a merge:

| Rule | Alerts | What it was |
| --- | --- | --- |
| `Google.Parens` | 1 | "Use parentheses judiciously" on the second paragraph (the "(most recently)" aside). |
| `Google.WordListCase` | 1 | "Use 'email' instead of 'Email'" on the contact list label. |

Every NellStyle rule reported 0 alerts. The exempt pages also report 0 Google alerts. That confirms a section-level `BasedOnStyles` in `.vale.ini` replaces the top-level list for those files, not adds to it.

## Known false positives

- **Heading case:** proper nouns not in the `exceptions` list are flagged. Add the name to `HeadingCase.yml`.
- **Product names:** lowercase `github` is not flagged on purpose. It appears in link text such as `github.com/nellcgram`, and Vale's regex engine has no lookahead to skip it.
- **Editor name:** quoting both names on purpose, for example in a naming comparison, triggers it.
- **Filler words:** "just" meaning "only" or "fair" is flagged.
- **Inflated words:** quoted text is flagged.
- **Passive voice:** it can flag passive wording that is deliberate, for example when the actor is unknown.
- **Sentence length:** long bullets and table rows are counted as one sentence.
- **Acronyms:** common terms that are not in the exceptions list are flagged. Add them to `Acronyms.yml`. Two-letter acronyms such as AI are not checked.
- **UI terms:** "login" as a noun is flagged as well.

## Exceptions

`.vale.ini` has three per-file sections. A section can switch rules off for matching files, and its `BasedOnStyles` replaces the top-level list for those files.

- **`docs/writing-samples/*.md`:** only NellStyle runs, so Google's rules are off. The heading-case, sentence-length and inflated-words rules are also off. These pages keep their published wording.
- **`docs/agentic-projects/docs-assistant.md`:** only NellStyle runs, with heading case and sentence length off.
- **`docs/writing-samples/eob-guide.md`:** heading case is off. The writing-samples section above already covers this file, so this section is redundant. It is kept because it records the original exception for the EOB guide's title-case headings.

Product-name and placeholder errors still run on every page, including the exempt ones.

Three Google rules are off everywhere: `Google.Headings`, `Google.Acronyms` and `Google.FirstPerson`. The first two duplicate NellStyle rules. The third would flag every "I" on this first-person site.

## Run it locally

```bash
vale sync
vale docs
```

CI installs the latest Vale (3.24.0 in the Oct 3 run) and syncs the current Google package on every run. Neither is pinned, so results can change without a commit.

## What can block a pull request

The Vale CI job fails only when an `error`-level alert lands on a line the pull request changes. NellStyle has two error rules: product names and placeholders. `.vale.ini` lowers `Google.EmDash` and `Google.Ordinal` from error to warning so they can't block either.
