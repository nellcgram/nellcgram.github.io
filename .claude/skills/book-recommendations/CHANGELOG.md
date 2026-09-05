## Changelog

### Commit: 3857bb6, [2026-09-04]
- Fixed: The skill checked for already-read.md but had no instruction 
  for a missing file, so it would recommend without the exclusion list 
  and nothing would signal the failure. Old: "Before you run the skill, 
  check already-read.md at [path]." New: Added, "If already-read.md is 
  not found at that path, stop. Tell the user the file is missing and 
  do not recommend anything. Never proceed without the exclusion list."
  
### Commit: [ef68341], [2026-09-04]
- Fixed: "Rules that alwways apply" needed an action added to rule that governs main character. Old: Main character could not rape or murder. New: Added main character cannot torture.

### Commit: [f36d2d7], [2026-09-04]
- Fixed: Two sections defined main-character eligibility differently, 
  giving the model conflicting authority on what a main character may 
  be. Old: "Rules that always apply" barred criminal main characters, 
  while "Content warnings" stated books may include rape, torture, or 
  murder if not committed by a main character — implying those three 
  acts were the boundary. New: Character eligibility is defined only 
  under "Rules that always apply." The content-warnings section governs 
  warning format and coverage only.

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