# Case study: Change My Room

Source: [github.com/nellcgram/room_change](https://github.com/nellcgram/room_change)

Try it: [Change My Room](https://nellcgram.github.io/room_change/)

Change My Room is a to-scale room planner for reworking a bedroom. You enter the room's size and doors, drag furniture into place, and give each piece a job. The app flags overlaps, pieces with no job, and zones that are missing something. Claude then reviews the layout and can edit it.

## What it does

- **Room setup:** width, length, and any number of doors or openings, in inches.
- **Furniture:** each piece has a real width and depth, a job (seating, storage, surface, light, footrest, decorative, or other), and any rotation angle.
- **Zones and issues:** furniture can be grouped into named zones such as "Reading Nook." A running list shows overlaps, pieces with no job, and zones missing something.
- **AI design review:** Claude reads a text description of the room and returns a critique with specific fixes.
- **Tell Claude what to change:** you describe a change in plain English, and Claude edits the furniture directly.
- **Critique & Fix Loop:** Claude critiques the room and lists suggestions. You pick one and review the exact changes it proposes. Nothing changes until you confirm. The app reports how the issue count changed and critiques the updated layout.

## How it is built

The app is plain HTML, CSS, and JavaScript with no build step. Furniture is drawn as SVG shapes, and collision checks use rotated-rectangle overlap math so pieces can sit at any angle. Layouts save to the browser's local storage, with a backup file option.

The page can't safely hold an API key, so the AI features call a small Cloudflare Worker that holds the key and forwards requests to Claude. The Worker accepts requests only from this site and caps usage at 100 requests a day across all visitors.

The [README](https://github.com/nellcgram/room_change#readme) in the repository covers setup.

Disclaimer: Draft written by Claude; edits by Nell pending
