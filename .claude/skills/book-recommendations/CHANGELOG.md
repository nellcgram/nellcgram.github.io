### Changelog

## Pre-git fix — missing frontmatter closing
- Fixed: Missing --- would have broken how the file's name and description got read. Old: The first draft of SKILL.md had an opening --- for the frontmatter but no closing ---. New: Added the missing closing --- after AI caught it.

## Pre-git fix — undefined TYPE field
- Fixed: A required field (TYPE) was missing from the format instructions so a later sentence referenced something undefined. Old: The format line read "ROLE, TIMING" (no TYPE), but the sentence "All four combinations of ROLE and TIMING are valid for each TYPE" referenced type which was undefined. The previous TYPE = "rape" or "sexual assault (not rape)" definition line was missing. New: Restored TYPE to the format line (TYPE (ROLE, TIMING)) and restored its definition line.

## Pre-git fix — Changed unclear wording
- Fixed: rewrote to produce better results. Old: "A current pregnancy in the plot is not allowed and the characters should not have children for most of the book, but can include epilogue baby/babies." New: "A current pregnancy in the plot is not allowed. Characters should not have children for most of the book. A baby or babies in the epilogue is optional."

## Commit: 467c3b1, [2026-08-31]
- Fixed: Duplicate entries give conflicting instruction for the model which confuses results. Old: Duplicate "rape/sexual assault" entry in the content-warning topics list in SKILL.md. New: Removed duplicate entry.

## Commit: cccbd9f, [2026-08-31]
- Fixed: Repeated and different wording gives conflicting instructions for the model which confuses results. Old: The pregnancy/children rule appeared twice, once under "Rules that always apply," and again as a shorthand duplicate under "Content": "No pregnancy, no kids for most of the book, epilogue baby optional." New: The pregnancy rule now exists only under "Rules that always apply." There is no other version of this rule in the content.

## Commit: 5c2041c, [2026-08-31]
- Fixed: Tightened the wording to make results accurate. old: The pregnancy/children rule read, "A current pregnancy in the plot is not allowed. Characters should not have children for most of the book. A baby or babies in the epilogue is optional." New: Under "Rules that always apply" it now says, "A main character should not have a child or pregnancy before the epilogue. A baby or babies in the epilogue is optional."