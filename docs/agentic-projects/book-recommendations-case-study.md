# Book Recommendations Skill

## The Skill

This is a skill that recommends romance novels. It filters out particular categories (novellas, mafia/vampire/demon/alien characters, anyone under 18, YA, small-town settings), excludes a list of specific authors I dislike, enforces a strict output format with content warnings, and does not announce what it filtered out.

## The Problem

Before I built the skill, Claude was giving me recommendations of authors I disliked, repeating authors in the list, and including books I had read already. Often there were not enough recommendations so I had to keep editing my prompt to Claude.

<details markdown="1">
<summary>Screenshots</summary>

Here is my first prompt.

![Initial prompt](../images/initial%20prompt.png)

Here is an example of the AI's visible searching:

![AI's visible searching](../images/searching%20visible.png)

Here is my first attempt to change project settings to get a more specific result.

![Trying to change project settings](../images/trying%20to%20change%20settings.png)

</details>

## What I Built
It only gives me recommendations I have not read, in my preferred format, in groups of 10 at a time.

<details markdown="1">
<summary>Screenshots</summary>

![Book Recommendations Skill 1](../images/1.png)

![Book Recommendations Skill 2](../images/2.png)

![Book Recommendations Skill 3](../images/3.png)

</details>

## How I Built It
I created the written skill in VS Code and tested it with Claude Code.

## Challenges

<details markdown="1">
<summary>Read the three rounds of debugging</summary>

In the first round of testing, I had a missing closing "---" that would have broken the file. I also had a sentence that contradicted itself (it said no children but also allowed for children in the epilogue).

In the second round, I realized the list of books I did not want recommended was huge and would make the skill too long to read easily, so I created the already-read.md file so I had a separate place to store past titles.

In the third round, results still included books I had read that I had not added to already-read.md initially. I edited the skill to add all recommendations to the "do not recommend" list after recommending them.

</details>

## Future Improvements

I am still considering whether the summary is necessary, and if it should be shortened.
