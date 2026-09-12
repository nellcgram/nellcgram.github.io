## Run 1 — [2026-09-04] (graded against run-01-output.md)

Grading limitation: this run was graded in the same session that 
produced the output, so the grader had the skill loaded. A grader with 
only the rubric and the raw output would be more reliable. Noted as a 
harness limitation, not a result.

Update, [2026-09-10]: Scored against SKILL.md and rubric.md as they stood before the 2026-09-12 edits (guardianship added, the "other books that qualify" note removed, the no-live-user genre fallback added). Differences from the current files are expected, not new defects.

Update, [2026-09-10]: this run was regraded by an independent agent 
given only the rubric, the exclusion file, and run-01-ouput.md — no 
SKILL.md, no prior grading, no case study. That pass caught a real 
defect this same-session grading missed twice (criterion 3, below) 
and exposed a wording gap in the rubric's criterion 4 (since fixed in 
rubric.md) that would otherwise misgrade every future run. Criterion 
12 is unchanged but now carries a flagged open question from that 
pass — see below.

- Criterion 1 (15 books): pass — 15 entries returned.
- Criterion 2 (real/attributed): fail — the model's output misattributed "The Suite Spot" to Mia Sosa; it's actually by Trish Doller. Verification (checking all 15 titles/authors, not just the 3-sample minimum, against publisher pages, Goodreads, and reviews) was done by Claude in-session; a manual spot-check of a subset by the grader is what actually caught this one.

  - FAILURE FOUND AND FIXED PRE-DELIVERY, GRADED AS A FAILURE ANYWAY: 
    the draft attributed "The Suite Spot" to Mia Sosa. It is by Trish 
    Doller. Hallucinated attribution — the defect criterion 2 exists 
    to catch. Caught during verification and swapped before the list 
    was delivered, but per the rubric's grade-what-was-produced rule 
    (see rubric.md), this run is still graded on the model's original, 
    uncorrected output. A caught-and-fixed error is not the same as a 
    run that never had the error, and grading the corrected version 
    would have hidden that.

- Criterion 3 (no pregnancy/child): fail — in *Life's Too Short* (Abby Jimenez), Vanessa Price, the main character, becomes her infant niece's sole guardian mid-book (her half-sister leaves the baby with her while dealing with addiction), not in an epilogue. Missed in the original grading; caught by an independent regrade and confirmed separately against plot summaries.
- Criterion 4 (not in already-read.md): pass — none of the 15 titles or authors appear in the specific-books or skip-all-authors sections of already-read.md as it stood before this run.
- Criterion 5 (not on skip-all-authors list): pass — cross-checked all 15 authors against the skip-all-authors section; no matches.
- Criterion 6 (no duplicate author): pass — 15 distinct authors.
- Criterion 7 (no novellas): pass — all 15 are full-length novels.
- Criterion 8 (no prohibited main-character types): pass — no criminal/mafia/vampire/demon/alien/serial-killer main characters; all contemporary-set.
- Criterion 9 (content-warning format/coverage): pass, with 2 unresolved low-confidence items with unverifiable (2 of 15 entries)
  - *Take the Lead* (Alexis Daria): outside sources describe the hero as "sexually harassed," but available reviews don't specify whether this rises to on-page sexual assault or stays verbal/non-physical harassment. The run included no content-warning line for this. If the scene involves physical contact, the entry is missing a `sexual assault (not rape) (main character, on page/past)` line and this criterion would fail for that entry.
  - *The Bodyguard* (Katherine Center): one source flagged "suicidal ideation" among the book's content but didn't identify which character it belongs to (Hannah's mother's backstory is the likelier candidate, per other sources' framing of that same backstory). The run omitted a mental-illness warning on the assumption it isn't the main character's. Unconfirmed from primary text.
  - No other entry showed evidence of an uncovered required topic (rape, torture, murder, cheating, BDSM, cancer, MC's dog dying) or a misformatted warning.
- Criterion 10 (heat level correctness): unverifiable (1 of 15 entries) — *The Matchmaker's List* (Sonya Lalli): no source found confirmed this as open- or closed-door; the run left off a heat-level line (defaulting to open-door), which is unverified either way.
- Criterion 11 (every entry has a link): pass — all 15 entries link to a real page for the title (Goodreads for 14; romance.io for *The Spanish Love Deception*, since no Goodreads URL was confirmed for it during the run).
- Criterion 12 (exclusion process invisible): pass — the response never mentions already-read.md, the skip-authors list, or why any book/author was excluded. Open question raised by an independent regrade, not yet resolved either way: six entries carry "Note: this author has other books that qualify," and "qualify" implies a pass/fail filter exists, which arguably reveals more than SKILL.md's own format example ("Note: This author has other books on this topic") does. Left as pass pending a decision on whether that wording crosses the line.

**Overall: 8 pass, 2 fail, 2 unverifiable (of 12 criteria).**
Unverifiable = criteria 9 and 10. Both need the book text; review-site 
summaries can't settle them.