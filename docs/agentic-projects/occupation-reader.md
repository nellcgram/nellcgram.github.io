# Case Study: A Blind-Reader Test for "Show, Don't Tell"

I built this to test whether a character's behavior shows their job without anyone stating it, and to practice designing and debugging a multi-agent workflow.

Source and full write-up: [github.com/nellcgram/blind-occupation-reader](https://github.com/nellcgram/blind-occupation-reader)

## What I built

- **A Claude Code skill with two agents.** A blind reader sees only the scene text and guesses the character's job. Five independent runs vote, and a second agent checks the winning answer against occupations I had already considered.
- **A web version.** A small Flask app does the same job, with a per-visitor rate limit, a daily cap, and a limit on text length. A Render blueprint is included. I have not deployed it.

The test character comes from a private manuscript, so the repository uses an invented sample character instead.

## Results

| What I measured | Result |
| --- | --- |
| Three runs on my manuscript, using different scene sets | A narrow answer, then a broad one, then the narrow one again |
| A correct re-run on the full manuscript | Matched the broad answer, 5 of 5 |
| Invented sample, two five-vote runs | Same answer both times, 5 of 5 |
| Runs that quoted a line stating the job, before and after a new rule | 1 of 5, then 0 of 5 |
| Cheapest model on the sample | Gave a nearby but different answer |

These come from one invented sample and a handful of runs. The sample is clear on purpose, so it shows that the pipeline works, not how it handles subtle writing.

## What I learned

1. **A tool restriction fixed a runaway-agent incident.** Parallel agents re-ran the whole workflow, and one pushed a deletion to an unrelated repository. They had shell access they never needed. Limiting them to reading files, plus a permission prompt before any push, fixed it.
2. **A changing answer was my input, not the model.** One run picked scenes by one of the character's two names and dropped the rest. Logging the exact text used for each run is what made that visible.
3. **The cheapest model missed the evidence.** Haiku 5.5 answered "paramedic" where the scenes point to a nurse. Sonnet 5.5 matched the strongest model, so it is the default.
4. **A rule helped but did not close the problem.** Telling the reader not to quote lines that state the job cut those quotes on the sample. Two of five runs still quoted a line about the schedule.

## Known limits

This is a prompt-based experiment, not a validated measure. Votes from one model are correlated, so five votes overstate independence. I did not compare the answers with human readers, and the web app's 13 tests use a fake model. The [case study](https://github.com/nellcgram/blind-occupation-reader/blob/main/docs/case-study.md) in the repository covers each limit and lists the next steps.
