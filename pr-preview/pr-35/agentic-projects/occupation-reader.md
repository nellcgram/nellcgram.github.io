# Case study: character job test

Source: [github.com/nellcgram/blind-occupation-reader](https://github.com/nellcgram/blind-occupation-reader)

This is my earliest project where Claude did the most work (creating agents with few instructions) to teach me the overall structure of system instructions. I’m including it to show my thought process.

## Introduction

I built this to solve a characterization problem. I wanted to submit all manuscript scenes to Claude, then have Claude figure out what job made the most sense for the character across scenes.

## Problems

1. I wanted the answer to come from the character’s psychology and behavior, not how he or other characters described him in dialogue, in case he was saying he was a soldier but was actually a spy.
2. I wanted a solution that allowed me to avoid adding the same scenes to each fresh Claude chat.
3. I was tired of constant prompt engineering, asking variations on the same questions.
4. I wanted to learn from Claude what system instructions worked best for this problem.

## Solutions

I asked Claude to build what it needed, then I rewrote the agent descriptions and prompts and used Claude Code to test results, and rewrote again. Each test I ran resulted in a new log of results and a new occupation considered.

The result is a Claude Code skill with two agents. Five independent readers see only the scene text, guess the job, and quote their evidence. A separate matcher compares the verdict with occupations I had already considered. Each run is logged with the exact text used.

My final problem was that this was not a project others could use because it used my own manuscript. I had Claude write sample scenes and rerun the tests so it made a new log and candidate file.

## What went wrong

While testing, parallel agents re-ran the whole workflow, and one pushed a deletion to an unrelated repository. The agents had shell access they never needed. I limited them to reading files and added a permission prompt before any push.

## What I did not measure

I did not compare the answers with human readers, test subtle or ambiguous writing (the sample is clear on purpose), or try other models.

The [README](https://github.com/nellcgram/blind-occupation-reader#readme) in the repository describes the agents. The [full technical case study](https://github.com/nellcgram/blind-occupation-reader/blob/main/docs/case-study.md) covers my design decisions and other problems I fixed.

## Conclusion

I ultimately decided that this was more work with Claude than it was worth. Testing the agents and skill and adjusting the writing took more time than my original prompt engineering and re-submitting scenes had.

The answer I settled on was to use less Claude in the writing process. I interrogated why I had been using Claude in the first place: to get a general sense of the character’s psychology from “someone else’s” perspective. I decided to write many more scenes, let the writing process determine what occupation seemed to fit best over time (possibly many months of writing and revising), and then take distance from the work before I assessed whether the occupation seemed accurate. This felt like a case of outsourcing my judgment to AI too much.

Disclaimer: Written partially by Claude, partially by Nell; edits by Nell
