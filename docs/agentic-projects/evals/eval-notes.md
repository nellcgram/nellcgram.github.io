# Eval notes

## Rubric defect: unverifiable is not pass

Found during Run 2.

**The problem:** The rubric only has pass and fail, so a criterion nobody can check resolves to pass by default. That means it reports "verified compliant" when the truth is "no contradicting evidence found.

**Which criteria are affected:** 9 and 10. Both need the book text; review sites don't carry heat level or precise content-warning detail.

**Why it matters:** A rubric that can't say "unknown" will report clean runs forever and stop being useful.

**How I'd close it:** I want all criterion to be used so I added unverifiable as a permanent third outcome that's counted separately.