# Case Study: Building and Evaluating Two Claude Code Skills

This is my first completed project to teach myself how to build an agentic AI skill, rubric, and eval harness. It shows that I can write precise specs for an AI, test them against a hand-written answer key, and tell whether a score reflects the model or my own documents.

Source and full write-up: [github.com/nellcgram/docs-assistant](https://github.com/nellcgram/docs-assistant)

## What I built

Two Claude Code skills for documentation work:

- **release-notes** turns git commit messages into user-facing release notes.
- **doc-review** reviews a document against a checklist.

I built a full evaluation around `release-notes`: 20 commits, a hand-written answer key, a graded rubric (a case passes only if it meets every criterion), scripted runs, and a GitHub Action that acted as a test gate, failing a push when quality dropped. The doc-review skill was checked by eye, and is less well-developed because it was used as proof of concept.

## What I learned

1. **My first 0 of 20 was my own documents disagreeing.** The rubric required past tense and no internal file names, and the skill never said either. Most of the climb to 19 of 20 was making the spec and the rubric agree, not the model improving.
2. **A passing test gate can be nearly blind.** I broke the skill five ways on purpose. Four of the breaks still passed, because the rules both skills read are repeated across files and the model followed those. Duplicated instructions make a prompt robust and its tests insensitive.
3. **How I called the skill changed the score more than most rule edits.** The same skill scored 20 of 20 with all commits in one request and 4 of 20 with one call per commit.
4. **The skill is right more often than it is consistent.** Across 5 repeats, only 9 of 20 cases passed every time, and my own run summaries turned out wrong until I graded one row per case.

## Known limits

All scores come from the 20 commits I tuned the skill against, so they don't show how it handles new ones. The [case study](https://github.com/nellcgram/docs-assistant/blob/main/case-study.md) in the repository has the CI screenshots, every other limit, and a link from each number to the file behind it.
