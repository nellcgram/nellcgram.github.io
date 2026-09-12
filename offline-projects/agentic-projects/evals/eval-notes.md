# Eval notes

## Rubric defect: unverifiable is not pass

Found during Run 1.

**The problem:** The rubric only has pass and fail, so a criterion nobody can check resolves to pass by default. That means it reports "verified compliant" when the truth is "no contradicting evidence found.

**Which criteria are affected:** 9 and 10. Both need the book text; review sites don't carry heat level or precise content-warning detail.

**Why it matters:** A rubric that can't say "unknown" will report clean runs forever and stop being useful.

**How I'd close it:** I want all criterion to be used so I added unverifiable as a permanent third outcome that's counted separately.

## Grading defect: scoring the corrected output, not the produced output

Found during Run 1.

**The problem:** Criterion 2 was graded pass because the delivered list already had "The Suite Spot" correctly attributed — the misattribution was caught and swapped before the run was scored. The grade reflected a hand-corrected result, not what the model actually produced.

**Which criteria are affected:** 2, and any criterion where an error could plausibly be caught and corrected before scoring.

**Why it matters:** If catching and quietly fixing an error resolves to the same grade as never having had the error, the score stops measuring the model's actual output — the same silent-clean-result problem the unverifiable outcome was meant to prevent.

**How I'd close it:** Added a rule to the rubric: grade what the model produced, not a corrected version. A caught-and-fixed error is logged separately but still fails that criterion for the run.

## Grading defect: same-session grading missed a real failure twice

Found when Run 1 was regraded by an independent agent given only the rubric, the exclusion file, and the raw output — no SKILL.md, no prior grading, no case study.

**The problem:** In *Life's Too Short*, the main character becomes her niece's guardian mid-book. Criterion 3 exists specifically to catch this, and it was graded pass — twice, across two separate same-session gradings — before an independently-run pass caught it. Same-session grading isn't just less reliable in theory; here it produced the same wrong answer on repeat.

**Which criteria are affected:** Any criterion requiring a careful read of the output against the rules, not just a records check. Criterion 3 is the confirmed case; there's no reason to assume it's the only one a same-session grader is prone to waving through.

**Why it matters:** A grading process that repeats its own mistake isn't self-correcting just because someone runs it again — it takes a genuinely separate check to surface what it's blind to.

**How I'd close it:** Regrade with an independent session or agent that never sees SKILL.md, the prior grading, or the case study — not as a one-time fix, but as a standing step for every run. The same pass also surfaced a second, distinct defect (below) that's worth its own entry.

## Rubric defect: already-read.md criterion didn't specify a pre-run snapshot

Found by the same independent regrade above.

**The problem:** The skill appends every recommendation to already-read.md right after delivering it, so the file's current state always contains the just-recommended titles. The rubric's wording for "no books or authors from already-read.md" didn't say to grade against the file as it stood *before* the run — so a grader working from the live file will always see this run's own titles sitting in it and misgrade a passing run as a fail.

**Which criteria are affected:** 4. Criterion 5 (skip-all-authors) is unaffected — that section isn't auto-appended to.

**Why it matters:** This isn't a rare edge case; it will misfire on every single future run until it's fixed, because the auto-append behavior it's tripping over is the skill's normal, intended behavior.

**How I'd close it:** Added wording to rubric.md specifying that criterion 4 grades against already-read.md as it stood before the run started, and explaining why, so a future grader isn't left to guess.

## Skill defect: instruction and rubric disagreed on what the rule was

Found by the same independent regrade that caught the guardianship 
failure in Run 1.

**The problem:** The rubric's criterion 3 already failed a run for a 
main character becoming a child's guardian mid-book. SKILL.md's own 
rule never mentioned guardianship — it only said "a child or 
pregnancy." The regrade worked because the rubric happened to be 
stricter than the instruction it was supposed to check; nothing 
forced the two to agree.

**Which criteria are affected:** 3. No other criterion is currently 
known to have language SKILL.md doesn't also state, but that hasn't 
been checked systematically — this one was found by coincidence, not 
by an audit.

**Why it matters:** A rubric can only check what an instruction 
actually says. Here it happened to check for more than the 
instruction covered, which looks like a rubric strength but is really 
two documents stating different rules under the same name.

**How I'd close it:** Added guardianship to SKILL.md's rule directly, 
so the instruction and the rubric state the same thing. Worth a pass 
checking whether any other rubric criterion is similarly ahead of, or 
behind, what SKILL.md actually instructs.