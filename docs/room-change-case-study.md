# Room Change

## Overview

[Room Change](https://nellcgram.github.io/room_change/) is a to-scale room planner I built to solve a real problem — my own bedroom felt cramped and I didn't like it — and it turned into an unplanned exercise in writing every touchpoint of a product from scratch: onboarding, in-app guidance, error recovery, and the instructions that shape an AI feature's voice and behavior.

## Why I built this

I didn't set out to build software. I wanted my room to feel less cluttered and stop being dominated by furniture I didn't like. That problem became the spec: a tool that lets someone drag furniture around a to-scale floor plan, flags real problems (blocked paths, storage with no purpose), and — eventually — lets an AI both critique the layout and make changes to it directly, in plain English.

## My role

I built this end-to-end working with Claude Code, an AI pair-programmer, over one long session. My role was every product and content decision: what the tool should do, how every visible string should read, what the app says when something goes wrong, and — since the tool eventually called an AI model itself — how to instruct that AI's tone, scope, and output format. The code implementation was AI-assisted; the judgment about what to say and how wasn't.

## Content decisions

### 1. Turning mechanical state into human meaning

Internally, the app just tracks a flag: a furniture item's `jobTag` is either something useful (`seating`, `storage`, `surface`...) or `"unassigned"`. The lazy version of that is a label like `unassigned_item_warning` — technically accurate, meaningless to a person deciding what to do about it.

Instead, that state gets translated into what it actually *means* for someone using the tool:

> *"Cedar Chest" has no job assigned — that's usually how a piece turns into a place to pile things.*

Same underlying fact. The difference is explaining *why it matters*, in a sentence a person would actually say.

### 2. Task-first labels, not developer language

Button copy can describe what the *system* does internally, or what the *person* is trying to do. Those aren't the same sentence. A button that creates a geometric no-furniture zone in the code could be labeled "Create Constraint" — accurate to the implementation, meaningless to the person using it. Instead:

| Says what the system does | Says what the person is doing |
|---|---|
| Create Constraint | **Mark a Clear Path** |
| Submit Prompt | **Tell AI What to Change** |

### 3. Recovery copy for failure states

**Before:** early on, a single missing element on the page could throw an error that silently stopped the app's startup code partway through. The room's data was completely safe in the browser's local storage the whole time — but the *screen* would just show an empty room, with nothing telling the person their real layout was fine and just wasn't displaying. That silence is exactly how a working save gets mistaken for lost data.

**After:** every part of the startup sequence runs independently now, and if any single piece fails, a banner appears instead of a blank screen:

> *Something didn't load right. Your saved room is almost certainly fine — try a hard refresh (Ctrl+Shift+R on Windows/Linux, Cmd+Shift+R on Mac) to fix it.*

It answers the only two questions a person in that moment actually has: *am I okay*, and *what do I click*.

### 4. Specific over vague in error messages

**Before:**

> *The AI service had a problem. Try again in a bit.*

Technically true, completely unhelpful — it gives no way to tell "your API key is wrong" from "you're out of credits" from "the model name is misspelled." **After:**

> *The AI service returned an error (status 400): "Your credit balance is too low to access the Anthropic API. Please go to Plans & Billing to upgrade or purchase credits."*

The specific version turned a dead end into a one-step fix — and it's the message that actually diagnosed the real issue during development, which the vague version had been hiding for several rounds of guessing.

### 5. Prompt writing as content design

Once the tool called an AI model to critique the room, the instructions telling that model *how to sound and what to prioritize* became a content artifact in their own right — no different in kind from writing a style guide, just for an AI audience instead of a human one.

**First version** — direct and grounded, for a practical critique:

> *You are a blunt, practical interior space-planning consultant... Be direct and specific, not diplomatic filler. No more than about 350 words. Write short plain paragraphs or a short bullet list.*

**Rewritten version** — after deciding the tool should brainstorm rather than just critique:

> *You are an imaginative interior designer... Give wildly creative, unconventional ideas... Output ONLY a bullet list. Extremely concise — fragments, not full sentences, as few words as possible per bullet.*

Same underlying task (respond to a room layout), completely different voice and output shape — controlled entirely through the written instruction, the same way a style guide controls a human writer's output.

## Outcome

The tool is live at [nellcgram.github.io/room_change](https://nellcgram.github.io/room_change/). It's a working example of content design applied past the usual surface — not just UI copy, but the error-recovery logic and the instructions steering an AI feature, treated as the same discipline.
