# Book Recommendations Skill

This project is about writing an unambiguous spec for an LLM, debugging it the way you'd debug conflicting requirements in any spec, and then building a rubric to check whether the model's output actually satisfies it. The example I used to practice this is a personal one: a Claude Code skill that recommends romance novels within a specific, fairly strict set of rules.

[The skill](https://github.com/nellcgram/nellcgram.github.io/blob/main/.claude/skills/book-recommendations/SKILL.md)

[The rubric](https://github.com/nellcgram/nellcgram.github.io/blob/main/docs/agentic-projects/evals/rubric.md)

[The changelog](https://github.com/nellcgram/nellcgram.github.io/blob/main/.claude/skills/book-recommendations/CHANGELOG.md)

[The eval run](https://github.com/nellcgram/nellcgram.github.io/blob/main/docs/agentic-projects/evals/run-01.md)

[The eval notes](https://github.com/nellcgram/nellcgram.github.io/blob/main/docs/agentic-projects/evals/eval-notes.md)

## The Problem

Before I built the skill, Claude was giving me recommendations of authors I disliked, repeating authors in the list, and including books I had read already. There were often not enough recommendations, so I had to keep editing my prompt by hand every time.

## What I Built

A written skill (SKILL.md) that encodes my preferences as rules: genre and content exclusions, an author exclusion list, a strict output format with content warnings, and a running record of books I've already been recommended so they aren't repeated. It returns 15 recommendations at a time, in my preferred format, without ever explaining what it filtered out or why.

<details markdown="1">

<summary>Screenshots</summary>

Here is what that looks like:

![Book Recommendations Skill 1](../images/1.png)

![Book Recommendations Skill 2](../images/2.png)

![Book Recommendations Skill 3](../images/3.png)

</details>

## How I Built It

I wrote SKILL.md in VS Code and tested it iteratively with Claude Code, running the skill, reading the output against my own rules, and editing the instructions when the output didn't match what I'd specified. Once the skill was stable, I wrote a scoring rubric with pass/fail/unverifiable criteria (real/attributed titles, no duplicate authors, content-warning coverage and format, and so on) and ran a full scored eval pass against a real set of output, logged in the eval run linked above.

## Challenges

In the first round of testing, I had two instruction defects. First, a missing closing "---" that would have broken the file. Second, a sentence that contradicted itself (it said no children but also allowed for children in the epilogue).

In the second round, the list of books I didn't want recommended had grown too large to keep inline — it would have made the skill file too long to read easily. I moved it into a separate already-read.md file, which is a progressive-disclosure fix: the exclusion list only loads when the skill actually runs, instead of bloating the instructions Claude reads every time.

In the third round, I found a state-persistence limitation in the model. Results still included books I had already read that hadn't made it into already-read.md yet. I edited the skill to add every recommendation to the "do not recommend" list immediately after recommending it, rather than relying on me to update it separately. That means already-read.md now also holds books that were only recommended, not necessarily read — the name is a holdover from before this fix and no longer fully describes what the file stores.

## How I Evaluated It

Passing my own read-through isn't the same as verifying the output against a fixed standard, so I wrote a 12-criterion rubric and scored a real run against it (see the eval run above). Two results from that pass stood out more than a clean scorecard would have:

- **A hallucination that the first score hid.** The model's draft attributed "The Suite Spot" to the wrong author. Claude checked all 15 titles and authors against publisher pages, Goodreads, and reviews in-session, and I spot-checked a subset by hand — the manual spot-check is what actually caught the misattribution. I corrected the entry before delivering the list, which meant the attribution criterion scored a clean pass: the rubric had graded the corrected output, not what the model produced. I fixed the rubric so it grades what the model actually produced — a caught-and-fixed error still fails that criterion for the run — and rescored Run 1 accordingly.
- **A defect in the rubric itself.** My first rubric only had pass and fail, which meant a criterion nobody could actually verify (like heat level, which isn't reliably documented anywhere outside the book's text) silently resolved to "pass." I added "unverifiable" as a distinct, separately-counted outcome so the rubric reports what's actually known rather than defaulting unknowns to clean.

Final score on Run 1: 9 pass, 1 fail, 2 unverifiable (of 12 criteria).

## Future Improvements

The run above was graded in the same session that produced the output, with the skill still loaded — a grader working from only the rubric and the raw output would be a more reliable check, and that's the next thing I'd change about the eval process. I'm also still deciding whether the book summary in each entry is necessary, and if not, cutting it.
