# Before you start: every tool, what it costs, and what is Windows-only

This page lists what my environment uses, what each tool is for, what it costs, and whether there is a free
alternative. You do **not** need all of it. **The starter kit needs only Claude Code and VS Code** (or just a chatbot,
for the tutor prompt). The two worked examples, each in its own repository, need more:
[ai-documentation-pipeline](https://github.com/david-giddyupdata/ai-documentation-pipeline) and
[ai-video-pipeline](https://github.com/david-giddyupdata/ai-video-pipeline). Each tool is also explained in one line
in [`GLOSSARY.md`](GLOSSARY.md).

"Recorded" means a figure from my own project records. "Listed" means a vendor or third-party price list, checked in
October 2026. Prices change: check every listed price before you buy.

> ## Adobe Premiere Pro is the one big paid item
>
> **Adobe Premiere Pro (Premiere Pro 2026, version 26.3) is a paid subscription and is required for the video
> example as built.** The starter kit doesn't need it. Listed at about **$22.99 a month on an annual plan billed monthly**, **$263.88 a year
> prepaid**, or **$34.99 a month with no annual commitment** (US individual prices, from third-party summaries of
> Adobe's pricing, 2026). The video pipeline drives Premiere through a custom panel, so it cannot be swapped for
> another editor without rebuilding that part. Everything in "Core environment" and most of "Documentation example"
> is free or something you may already own.

**Platform.** My environment runs on Windows 11. Rows marked **Windows-only** have no drop-in replacement on macOS or
Linux.

**How the agent drives each tool.** Harness = the agent tool itself. Browser = browser automation (Playwright over
the Chrome DevTools Protocol). API = the vendor's web API. WS = a local websocket connection (a live two-way link
between two programs on the same computer). Bridge = a plugin inside the app that takes the agent's commands and
carries them out. Code = the agent writes code that renders the output. File = the agent writes a file the app
imports. OS = Windows UI automation. COM = Windows' built-in way for one program to control another. Library = a
Python or Node package the agent's scripts call. Human = I do it by hand.

---

## Core environment

What anyone needs before either example. The starter kit needs only the first and fourth rows (Claude Code and
VS Code).

| Tool | What it's for | Required? | Paid or free, with price | Free alternative | How the agent drives it |
|---|---|---|---|---|---|
| **Claude Code** (in VS Code or the Claude desktop app) | The agent: plans, writes and runs every script, hands work to helper agents | Required | Needs a paid Claude plan. Listed: Pro $20 a month ($17 on an annual plan), Max $100 or $200 a month; the free Claude tier doesn't include Claude Code | Other agent tools exist, and many read `AGENTS.md`; the practices here are tool-neutral | Harness |
| Claude models (Opus, Sonnet, Haiku, Fable) | Coordinator; reviewer; the "AI student"; quick checks | Included with the Claude plan | Recorded: no cash cost on top of the plan | n/a | Harness (helper agents started by instruction) |
| Claude Code Remote Control | Approve and steer from a phone | Optional | Included with the plan | n/a | Harness |
| **Visual Studio Code** | The editor that hosts Claude Code | Required for Claude Code in an editor | Free | n/a | Human |
| **Git** and a GitHub account | Version history | Required for the examples; not for the starter kit (download the ZIP instead) | Free | n/a | CLI |
| **Python 3** | Every example script | Required for the examples | Free | n/a | CLI |
| **Playwright** (Python) | Drives a real browser | Required for the examples | Free, open source | n/a | Library (Browser) |
| Microsoft Edge or Google Chrome, in separate profiles on their own debugging ports | Keeps the agent's browsing away from your everyday browser and logins; you sign in yourself | Required for the examples | Free | n/a | Browser |
| A secrets store (I use AWS Secrets Manager, read through a small helper) | Keys read at run time; never pasted into a prompt or a file | Required (some secrets store) | Recorded: AWS-billed, small | Your operating system's keyring, for example Python's `keyring` package | API |
| OpenRouter | One account for outside models (Gemini, GPT, image models) | Optional | Pay per use at the provider's list price, plus 5.5% on credits bought by card (minimum $0.80). Recorded: about $11.50 across all my video work | Call providers directly with your own keys | API |

## Documentation example (its own repository)

For rebuilding a Word manual from a master copy, capturing and annotating screenshots, and testing the manual
against the live product.

| Tool | What it's for | Required? | Paid or free, with price | Free alternative | How the agent drives it |
|---|---|---|---|---|---|
| **python-docx** | Rebuilds the draft from a never-edited master; edits by style; layout passes | Required | Free | n/a | Library (Code) |
| **Microsoft Word** (through COM, Windows' way for one program to control another) | Renders the draft to PDF for checking | Required as built | Paid (part of Microsoft 365) | LibreOffice in headless mode can render .docx to PDF (not tested with these scripts) | OS (COM) |
| PyMuPDF | Renders and checks pages: blank pages, numbering, contact sheets | Required | Free (AGPL license; see `THIRD_PARTY.md`) | n/a | Library |
| Pillow | Snagit-style annotation: boxes, arrows, numbered circles, torn edges, cuts | Required | Free | n/a | Library (Code) |
| **Tesseract OCR** | Reads text in images during the build | Required as built (set `TESSERACT_CMD` if it isn't in `C:\Program Files\Tesseract-OCR\`) | Free | n/a | CLI |
| Chrome on its own debugging port, with an isolated profile | The browser the manual is walked and captured in | Required | Free | Edge | Browser |
| Raw DevTools screenshots (`Page.captureScreenshot`) | Double-resolution captures with every element's position saved, so annotations are computed | Required | Free | n/a | Browser |
| The "student" tool server (a small local server in the documentation repository) | Gives the AI student see-only tools: screenshot, click, drag, type, scroll | Optional (for AI-student testing) | Free | n/a | Browser, through the server |
| AWS CLI | Listing objects and deleting by name in the product being documented | Optional (specific to this product) | Free tool; your AWS account costs apply | n/a | CLI |
| The product you document (mine: QuickSight (AWS)) | What the manual teaches | Your own | Your own account's costs | Any product you document | Browser |

## Video example (its own repository)

For turning the manual into a narrated, edited video with an optional avatar.

| Tool | What it's for | Required? | Paid or free, with price | Free alternative | How the agent drives it |
|---|---|---|---|---|---|
| **Adobe Premiere Pro 2026 (26.3)** | My review and finishing tool; the pipeline builds each round's project, captions and markers, and exports check frames | **Required as built** | **PAID.** About $22.99 a month (annual plan, billed monthly), $263.88 a year prepaid, or $34.99 a month with no commitment (listed, third-party, 2026) | DaVinci Resolve has a free edition, but the Premiere panel would not carry over (not tested). Remotion alone can render a finished file, without the human finishing step | Bridge (a custom panel with a local, token-guarded server) and File (XML timelines, captions). Unsigned Adobe panels must be allowed through a registry value |
| **OBS Studio** and obs-websocket | Records the capture screen in its own profile, then restores yours | Required | Free, open source | n/a | WS (local, password from the secrets store) |
| **ElevenLabs** | Narration in a clone of your own voice | Required for a cloned voice | Paid. Listed: Starter $6, Creator $22, Pro $99 a month. Instant clones need Starter or above; professional clones need Creator or above, your own voice only, verified | `edge-tts` (a free Microsoft voice, not yours) as a placeholder | API |
| `edge-tts` | Free placeholder voice for early drafts | Optional | Free (check the service's terms) | n/a | Library |
| **Remotion** (React, TypeScript) and Node.js | Draws the cursor, click rings, zooms, overlays, chapter cards | Required | Free for individuals and companies of up to 3 people; companies of 4 or more need a paid company license (remotion.dev/license) | n/a | Code |
| A forced-alignment model (Qwen3-ForcedAligner-0.6B) | Exact word timings for cuts, captions and click cues | Required | Free (Apache-2.0); a graphics card helps | Vosk (older, less exact) | Library (local model) |
| BiRefNet through `rembg` | Cuts generated art out of its background | Optional | Free (MIT) | n/a | Library (local model) |
| RapidOCR | Second text reader where Windows OCR fails | Required as built | Free (Apache-2.0) | Tesseract | Library (local model) |
| Windows OCR | Reads still frames for the line check and the privacy scan | Required as built | Free, built in. **Windows-only** | RapidOCR or Tesseract alone | OS |
| ffmpeg / ffprobe | Click repair, frame pulls, joins, loudness | Required | Free | n/a | CLI |
| OpenCV, NumPy, Pillow | Frame analysis, sync flashes, image work | Required | Free | n/a | Library |
| Windows UI Automation (`comtypes`), `pywin32` | Drives the file Open dialog; clears the capture screen | Required as built | Free. **Windows-only** | n/a | OS |
| **HeyGen** | Avatar intro, outro and picture-in-picture | Optional (leave the avatar out) | Paid. Listed: Free $0, Creator $29, Pro $49 a month. Recorded: four API test renders cost $0.40 | Leave the avatar out | API |
| An outside model for a blind frame review (Gemini, through OpenRouter) | One independent check per video | Optional (recommended) | Pay per use. Recorded: about $5.40 for one video's review | A fresh Claude helper agent on the plan, a weaker outside view | API |
| Image models (through OpenRouter) | Prop and background candidates (none shipped) | Optional | Pay per use. Recorded: 5 images $0.24, backgrounds $0.61 | Your own photos and art (what actually shipped) | API |
| YouTube Data API | Private uploads only; you publish by hand | Optional | Free | Upload by hand | API |

---

## What my recorded spend looks like

| Item | Figure |
|---|---|
| All outside model calls for the video work so far (OpenRouter) | About $11.50, under a $25 cap |
| One blind outside frame review | About $5.40 |
| Four avatar test renders (HeyGen API) | $0.40 |
| Subscriptions in use | A Claude plan, Premiere Pro, ElevenLabs, HeyGen Pro ($49), Microsoft 365 |

The outside API calls are small. The subscriptions are the real cost, and Premiere Pro is the largest single line
someone reproducing the video example would add.

## Not confirmed

- Premiere Pro and Claude plan prices come from third-party 2026 summaries, not the vendors' own pages.
- ElevenLabs plan prices are third-party.
- LibreOffice and DaVinci Resolve as replacements are untested with these examples.
