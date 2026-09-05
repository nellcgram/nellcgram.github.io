# Book recommendations skill

## What it does

## Files
- SKILL.md — the instruction file
- already-read.example.md — template for the private exclusion file
- Changelog: Talks about what was changed and why

## The private dependency
already-read.md lives outside this repo at 
~/.claude/private-notes/book-recommendations/. It's personal reading 
history and is deliberately never committed. Copy the example file to 
that path to use the skill.

## How to add an exclusion

## What breaks it

## Note on repo history

Commit 4a449f80 ("Delete already-read.md from github history") did 
not remove anything from history — a normal commit can't. The file 
was actually removed from history later via git filter-repo. Noting 
this so the commit log stays honest.