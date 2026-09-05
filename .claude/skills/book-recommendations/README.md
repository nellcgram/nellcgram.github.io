# Book recommendations skill

## What it does
Recommends full-length contemporary and fantasy romance novels 
against a fixed set of rules: no novellas, no prohibited main-character 
types (criminal, mafia, vampire, demon, alien, serial killer), no 
pregnancy or child for a main character before the epilogue, and no 
repeated or already-read authors. Every entry includes a link, a 
content-warning line where required, and a heat-level note for 
closed-door books. The exclusion process runs invisibly — the 
response never explains what was filtered out or why.

## Files
- SKILL.md — the instruction file
- already-read.example.md — template for the private exclusion file
- ../evals/rubric.md — the 12-criterion evaluation rubric
- ../evals/run-01.md — graded results from the first eval run
- ../evals/changelog.md — what changed in SKILL.md, and why

## The private dependency
already-read.md lives outside this repo at 
~/.claude/private-notes/book-recommendations/. It's personal reading 
history and is deliberately never committed. Copy the example file to 
that path to use the skill.

## How to add an exclusion

Tell the skill directly — mention a new author or book you've read or 
want avoided, and it adds the entry to already-read.md automatically. 
After every set of recommendations, the skill also appends each 
recommended title to already-read.md on its own, so nothing gets 
suggested twice without you asking for it.

To exclude an author from every future run regardless of what you've 
read, add them under "## skip all books by these authors:" in 
already-read.md directly.

## What breaks it

- A missing closing `---` in the frontmatter breaks how the file's 
  name and description get read.
- Two sections defining the same rule differently — the pregnancy 
  rule once existed in two places with slightly different wording, 
  which gave the model conflicting instructions.
- A missing already-read.md at the expected path used to fail 
  silently, recommending without any exclusion filtering. Fixed: the 
  skill now stops and says the file is missing rather than proceeding.
- The exclusion list and the recommend-and-record step are separate 
  actions — if a run doesn't finish, newly recommended titles may not 
  get written back to already-read.md, and could be recommended again 
  next time.
  
## Note on repo history

Commit 4a449f80 ("Delete already-read.md from github history") did 
not remove anything from history — a normal commit can't. The file 
was actually removed from history later via git filter-repo. Noting 
this so the commit log stays honest.