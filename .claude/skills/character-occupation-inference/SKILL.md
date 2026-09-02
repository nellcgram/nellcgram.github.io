---
name: character-occupation
description: Use this when the user wants to infer a character's job or role from a scene, based on his behavior and psychology rather than anything stated outright — including when the character claims a different occupation than his actions support.

---

You will be given the text of one or more scenes for a specific character.

1. Run the blind-inferrer agent 5 separate times. Give each run only the scene text — no other context, no memory of the other runs, no prior entries for this character.

2. Collect all 5 results (each an Answer plus its Why quotes).

3. Count how many runs gave each Answer. Report the plain count (e.g., "3 intelligence, 2 military") — never add a label like "confident" or "unclear" on top of the numbers.

4. Take the Answer with the most votes as today's result. Use the Why quotes from the runs that picked it.

5. Check whether a log file already exists for this character (data/logs/<character>.md). If it does, read its most recent entry.

6. If a previous entry exists, compare today's scene text and Answer to it. State plainly what's different in the text, and whether the Answer changed from last time.

7. Append a new entry to the character's log file, formatted like this:

   ## [today's date]
   - Answer: [occupation] ([vote count], e.g. 3/5)
   - Why: [quoted lines]
   - Scene text: [the exact text used for this run]

8. Run the matcher agent, giving it today's Answer + Why and the character's candidates.md file. Report back whether it matches an existing entry, is new, or contradicts one — citing the specific entry either way.

9. Report to the user: the Answer, the vote count, the Why quotes, what changed since last time (if there was a last time), and the matcher's finding.