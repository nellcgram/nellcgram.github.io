# Room planner

This was my first experimental project with Claude in an attempt to make something agentic. I realized through creating this project that it wasn't useful to me; it was more work than drawing out options on a piece of paper but not any more effective. But creating this project helped me understand what Claude Code could do.

Below is the explanation of what the app does.

## Case study

Source: [github.com/nellcgram/room_change](https://github.com/nellcgram/room_change)

You can [try the app](https://nellcgram.github.io/room_change/) in your browser.

Change My Room is a to-scale room planner for reworking a bedroom. You enter the room's size and doors, drag furniture into place, and give each piece a job. The app flags overlaps, pieces with no job, and zones that are missing something. Claude then reviews the layout and can edit it.

## What it does

- Room setup takes a width, a length, and any number of doors or openings, in inches.
- Each piece of furniture has a real width and depth, any rotation angle, and a job: seating, storage, surface, light, footrest, decorative, or other.
- You can group furniture into named zones, such as "Reading Nook." A running list shows overlaps, pieces with no job, and zones that are missing something.
- The AI design review sends a text description of the room to Claude, which returns a critique with specific fixes.
- "Tell Claude what to change" takes a plain-English request, and Claude edits the furniture directly.
- The Critique & Fix Loop has Claude critique the room and list suggestions. You pick one and review the exact changes it proposes. Nothing changes until you confirm. The app then reports how the issue count changed and critiques the updated layout.

## How it's built

The app uses plain HTML, CSS, and JavaScript with no build step. It draws furniture as vector shapes, and collision checks use rotated-rectangle overlap math so pieces can sit at any angle. Layouts save to the browser's local storage, with a backup file option.

A web page can't safely hold an API key, so the AI features call a small Cloudflare Worker. The Worker holds the key and forwards requests to Claude. It accepts requests only from this site and caps usage at 100 requests a day across all visitors.

The [README](https://github.com/nellcgram/room_change#readme) in the repository covers setup.

Disclaimer: written by Claude, edits by Nell
