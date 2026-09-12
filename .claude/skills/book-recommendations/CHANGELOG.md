## Changelog

### Edited SKILL to differentiate between live user and tool [2026-09-12]
- Fixed: Added wording for situation if there is no live user. Old: "If the user does not mention it, Claude should ask for each request: What genre?" New: "If the user does not mention it, ask which genre. If there is no live user turn to ask (e.g. an automated or eval run), default to contemporary and state that the default was applied."

### Edited README "what it does" section [2026-09-12]
- Fixed: README "what it does." Old: Contemporary and fantasy genres. New: "giving options of genre (contemporary, fantasy, historical, regency, romantic suspense, something else)" and added "no guardianship" to child requirements.

### Edited skill formatting [2026-09-12]
- Fixed: spacing, grammar.

### Deleted "other books that qualify" line of skill [2026-09-12]
- Fixed: The "note if you found other books by an author that qualify" instruction conflicted with the invisible-exclusion rule. "Qualify" implies a pass/fail filter, which tells the reader a screening process exists — the exclusion rule requires that the response never reveal what was filtered or why. Run 1 produced six entries carrying this note; Run 2 produced none, so the instruction was already inconsistently applied. Old: "Include only 1 book by each author, but note if you found other books by an author that qualify." New: "Include only 1 book by each author." Format example updated to drop the "Note:" line.

### Added guardianship to skill's pregnancy/child rule [2026-09-12]
- Fixed: The rubric already failed a run for a main character becoming a child's guardian mid-book, but SKILL.md's rule only covered pregnancy and having a child — the two documents disagreed about what the rule was. Old: "A main character should not have a child or pregnancy before the epilogue." New: "A main character should not have, be pregnant with, or be the guardian of a child before the epilogue." The rubric's wording didn't need to change; it already stated this.

### Doc fix — broken rubric link and missing eval links, [2026-09-10]
- Fixed: The case study's "The rubric" link pointed to 
  .claude/skills/book-recommendations/rubric.md, which doesn't exist — 
  the rubric lives under docs/agentic-projects/evals/. Old: Link 
  targeted a nonexistent path. New: Link retargeted to 
  docs/agentic-projects/evals/rubric.md, and links to the eval run 
  (run-01.md) and eval notes (eval-notes.md) were added alongside it, 
  since the case study didn't reference the eval work at all.

### Doc fix — typo in this changelog, [2026-09-10]
- Fixed: "Rules that alwways apply" typo in the [ef68341] entry above. 
  Old: "alwways". New: "always".

Note: commit hashes dated before 2026-09-04 are stale. History was 
rewritten on that date with git filter-repo to remove a privately 
committed file. Dates in this log remain accurate; hashes before the 
rewrite do not resolve.

### Commit: 3857bb6, [2026-09-04]
- Fixed: The skill checked for already-read.md but had no instruction 
  for a missing file, so it would recommend without the exclusion list 
  and nothing would signal the failure. Old: "Before you run the skill, 
  check already-read.md at [path]." New: Added, "If already-read.md is 
  not found at that path, stop. Tell the user the file is missing and 
  do not recommend anything. Never proceed without the exclusion list."

### Commit: [ef68341], [2026-09-04]
- Fixed: "Rules that always apply" needed an action added to rule that governs main character. Old: Main character could not rape or murder. New: Added main character cannot torture.

### Commit: [f36d2d7], [2026-09-04]
- Fixed: Two sections defined main-character eligibility differently, 
  giving the model conflicting authority on what a main character may 
  be. Old: "Rules that always apply" barred criminal main characters, 
  while "Content warnings" stated books may include rape, torture, or 
  murder if not committed by a main character — implying those three 
  acts were the boundary. New: Character eligibility is defined only 
  under "Rules that always apply." The content-warnings section governs 
  warning format and coverage only.

### Commit: 4a449f8, [2026-09-04]
- Fixed: already-read.md's path pointed inside the repo, risking the 
  private exclusion file being committed alongside the skill. Old: 
  "Before you run the skill, check already-read.md in this same 
  folder." New: "Before you run the skill, check already-read.md at 
  /Users/nellgram/.claude/private-notes/book-recommendations/already-read.md 
  (this file lives outside the git repo on purpose and must never be 
  copied into the repo or committed)."

### Commit: 7bd4a1a, [2026-09-01]
- Fixed: The exclusion instruction pointed to "the matching list 
  above," but no such list exists in this file — already-read.md is 
  external. Old: "If the user mentions a new author or book they've 
  read or want avoided, add it to the matching list above so it's 
  remembered next time." New: "If the user mentions a new author or 
  book they've read or want avoided, add it to already-read.md so 
  it's remembered next time."

### Commit: 467c3b1, [2026-08-31]
- Fixed: Duplicate entries give conflicting instruction for the model which confuses results. Old: Duplicate "rape/sexual assault" entry in the content-warning topics list in SKILL.md. New: Removed duplicate entry.

### Commit: 5c2041c, [2026-08-31]
- Fixed: Tightened the wording to make results accurate. old: The pregnancy/children rule read, "A current pregnancy in the plot is not allowed. Characters should not have children for most of the book. A baby or babies in the epilogue is optional." New: Under "Rules that always apply" it now says, "A main character should not have a child or pregnancy before the epilogue. A baby or babies in the epilogue is optional."

### Commit: cccbd9f, [2026-08-31]
- Fixed: Repeated and different wording gives conflicting instructions for the model which confuses results. Old: The pregnancy/children rule appeared twice, once under "Rules that always apply," and again as a shorthand duplicate under "Content": "No pregnancy, no kids for most of the book, epilogue baby optional." New: The pregnancy rule now exists only under "Rules that always apply." There is no other version of this rule in the content.

### Pre-git fix — Changed unclear wording, [2026-08-31]
- Fixed: The rule forebade children, then permitted one. Edited for consistency. Old: "A current pregnancy in the plot is not allowed and the characters should not have children for most of the book, but can include epilogue baby/babies." New: "A current pregnancy in the plot is not allowed. Characters should not have children for most of the book. A baby or babies in the epilogue is optional."

### Pre-git fix — undefined TYPE field, [2026-08-31]
- Fixed: A required field (TYPE) was missing from the format instructions so a later sentence referenced something undefined. Old: The format line read "ROLE, TIMING" (no TYPE), but the sentence "All four combinations of ROLE and TIMING are valid for each TYPE" referenced type which was undefined. The previous TYPE = "rape" or "sexual assault (not rape)" definition line was missing. New: Restored TYPE to the format line (TYPE (ROLE, TIMING)) and restored its definition line.

### Pre-git fix — missing frontmatter closing, [2026-08-31]
- Fixed: Missing --- would have broken how the file's name and description got read. Old: The first draft of SKILL.md had an opening --- for the frontmatter but no closing ---. New: Added the missing closing --- after AI caught it.