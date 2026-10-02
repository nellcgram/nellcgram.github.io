# NellStyle: custom Vale rules

These rules run on top of the [Google developer documentation style guide](https://developers.google.com/style) package. `.vale.ini` loads both, so a page is checked against Google's rules and these.

Severity decides what blocks a pull request. Only `error` rules fail CI. `warning` and `suggestion` alerts show up as annotations and never block a merge.

## Rules

| Rule | File | Severity | What it flags |
| --- | --- | --- | --- |
| Heading case | `HeadingCase.yml` | warning | Headings that are not sentence case (the pronoun "I" and listed proper nouns are allowed) |
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

These counts come from the Vale job on PR #13, the first real run (Vale could not run in the authoring environment, so nothing earlier was tested). Counts are for `docs/` after the fixes in the second commit.

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

False positives still present:

- **"is unresolved" in `docs-assistant.md`** is flagged as passive voice, but "unresolved" is an adjective.
- **`Google.WordListCase`, `Google.Colons`, `Google.Will` and `Google.Contractions`** produce many warnings on this site's deliberate wording. They are Google rules, not NellStyle rules, and none blocks a merge.

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

- `docs/writing-samples/eob-guide.md` is exempt from the heading-case rule. It keeps title-case headings. The exception is a section in `.vale.ini`.
- `Google.Headings`, `Google.Acronyms` and `Google.FirstPerson` are off everywhere. The first two duplicate NellStyle rules. The third would flag every "I" on this first-person site.

## Run it locally

```bash
vale sync
vale docs
```

## What can block a pull request

The Vale CI job fails only when an `error`-level alert lands on a line the pull request changes. NellStyle has two error rules: product names and placeholders. `.vale.ini` lowers `Google.EmDash` and `Google.Ordinal` from error to warning so they cannot block either.
