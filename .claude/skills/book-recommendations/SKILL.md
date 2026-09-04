---
name: book-recommendations
description: Use this when the user asks for book recommendations.

---

## Rules that always apply

- Only recommend full-length novels — no novellas.
- No criminal or mafia main characters, no vampires, no demons, no aliens, no serial killers.
- No main character under 18, no high school settings, nothing in the YA category.
- No main character who rapes, molests, stalks, or kidnaps another character.
- The romance must be between a man and a woman.
- A main character should not have a child or pregnancy before the epilogue. A baby or babies in the epilogue is optional.
- Always state the author's name with every book, and double-check the author matches the book; don't mix authors up.
- Include only 1 book by each author, but note if you found other books by an author that qualify.

## Check before running
Before you run the skill, check already-read.md at /Users/nellgram/.claude/private-notes/book-recommendations/already-read.md (this file lives outside the git repo on purpose and must never be copied into the repo or committed).

## Running, filtering and updating
Keep the exclusion-checking invisible. Never mention the excluded-authors list, the already-read list, or why a book/author was skipped. Just present the final clean list of recommendations.

Recommend only real, published romance novels. Verify each title and author exist before listing them, and say so if you can't confirm one.

Every recommendation should include a link to the title.

If the user mentions a new author or book they've read or want avoided, add it to already-read.md so it's remembered next time.

The recommendation should include no value judgments on Claude's part about the content.

After giving the final list of recommendations, add each one to already-read.md in the same format as the rest before you end your reply.

## Content warnings

If a book is closed door, note that. If it's open door, do not note it.

Each entry must include content warnings for these topics: rape, torture, murder, cheating, BDSM, cancer, main character's dog dies, main character with PTSD or other mental illness

If there are no content warnings, do not include that line.

Content warnings for sexual violence use the format:
  TYPE (ROLE, TIMING)

TYPE = "rape" or "sexual assault (not rape)"
ROLE = "main character" or "secondary character"
TIMING = "on page" or "past"

All four combinations of ROLE and TIMING are valid for each TYPE.

Examples:
  rape (main character, on page)
  rape (secondary character, past)
  sexual assault (not rape) (main character, on page)

## Format

Format of the response should be: 15 books minimum, or a reason why 15 is not possible

If the user does not mention it, Claude should ask for each request: What genre (contemporary, fantasy, historical, regency, romantic suspense, etc)?

## Format example
**Not the Girl You Marry** [Link], Andie J. Christopher.
Genre: Contemporary
A PR executive who ghostwrites a men's dating column ropes a charming photographer into "research" for her articles.
Content warnings: Rape (main character, past), cancer
Heat level: Closed door.
Note: This author has other books on this topic.