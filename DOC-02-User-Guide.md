# DOC-02 User Guide (Learner)

| | |
|---|---|
| **Author** | Iain Reid |
| **Classification** | INTERNAL |
| **Owner** | Support Lead (deputy: CONFIRM) |
| **Version** | 2.0 draft |
| **Date** | 2026-11-20 |
| **Governing documents** | [PRD](../../prd.md) s4, [DOC-10 UI Guide](DOC-10-User-Interface-Guide.md) |
| **Status** | Written from the PRD and routes in `app.py`. Not walked through on a running system |

> Features marked **(not wired)** exist in the engine or schema but have no route in `app.py` today (DOC-01 G-09). Do not rely on them until DOC-13 shows them passing.

## 1. Start a session

1. The operator starts the container and gives you the line `Ready: http://127.0.0.1:<port>/?token=<hex>`.
2. Open it in Firefox ESR or Chromium on the same host. The address bar then shows the page without the token.
3. Only one browser session can be active. A second one is refused (HTTP 409) **once the 409 rule is fixed (G-01)**.
4. After the idle time (default 60 minutes) the next click returns HTTP 401. Ask the operator to restart the container for a new link.

## 2. Translate

| Step | Action |
|---|---|
| 1 | Choose the direction yourself: EN to LA or LA to EN. The system never guesses |
| 2 | Choose a level 1 to 6 or Barbarian Mode (EN to LA only) |
| 3 | Type or paste up to 512 tokens. Longer input is refused with the count and nothing is translated |
| 4 | Submit. The "Processing" badge shows while it runs (needs JavaScript) |
| 5 | Optional: thumbs up or down on the result |

Notes:

- The tool removes control characters and the characters `; & | $ < > \` and the backtick from your text. If it changed anything you are told "input sanitised".
- `[FALLBACK: word]` in the output means the dictionary did not know the word. It is a warning, not a translation.
- Strict mode prints `[UNKNOWN: word]` and returns no partial text **(not wired: the profile setting is not read yet)**.

## 3. Reading levels

| Level | Name | Ages |
|---|---|---|
| 1 | Beginner | 2 to 4 |
| 2 | Elementary | 5 to 6 |
| 3 | Primary | 7 to 8 |
| 4 | Intermediate | 8 to 12 |
| 5 | Secondary | 12 to 16 |
| 6 | Advanced | 16 to 18 and adult |
| Barbarian | Stylistic register | Any |

You can change level at any time, up and down. The level is remembered per profile.

## 4. Profiles

Create, choose and delete profiles on the Profiles page. Delete asks for confirmation and overwrites the file. Rename **(not wired)**. Each profile is separate; nothing is shared.

## 5. Speech (TTS)

Latin is spoken with espeak-ng after a phonetic mapping (long vowels held, C as K, V as W). Modes: `playback` (to the speaker), `export` (a WAV download), `both`. A new request stops the one playing.

## 6. Printable PDFs

Workbook (alternating lines with writing space), declension grid, note-taking margins. Paper is A4 or Letter. The PDF is downloaded, never stored by the app.

## 7. Dashboard and clearing data

The Dashboard shows counts of translations and sessions. Word-friction lists and history **(partly wired)**. "Clear Telemetry" deletes history, friction, ratings, proficiency and error records for the active profile only, permanently.

## 8. Importing text **(not wired)**

The PRD describes `.txt`, `.md` and `.csv` import in 50,000-character chunks. No route exists yet.

## 9. Getting help

See [DOC-04](DOC-04-Support-Tasks.md). Report the time (UTC) and what you pressed; do not paste long text into a ticket.

## Sources

[PRD](../../prd.md) s4.1 to s4.7; `app.py` routes; `engine/sanitiser.py`; `engine/reading_age.py`.
