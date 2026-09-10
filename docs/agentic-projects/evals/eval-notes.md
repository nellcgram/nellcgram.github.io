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