# Glossary: every tool from the talk, one line each

Grouped by the mind map's five branches. Prices are as of October 2026, mostly from vendor or third-party price
lists; check before you buy. "My spend" is what my own records show. You don't need most of this: the starter kit
needs only Claude Code and VS Code (see `README.md`).

## Workspace

| Term or tool | What it is | Cost |
|---|---|---|
| Project folder | One folder per real project. The work lives in its files, so it outlives the chat and another agent can pick it up | Free |
| Visual Studio Code (VS Code) | A free editor that puts the agent chat, your document and your folder on one screen | Free |
| Extension | An add-on for VS Code. Example: Rainbow CSV colors the columns of a data file | Most are free |
| Claude Code | Anthropic's AI agent. It runs inside VS Code (or the Claude desktop app), reads and writes files, and runs programs | Needs a paid Claude plan: Pro about $20 a month, Max $100 or $200. The free plan doesn't include it |
| Claude desktop app | Anthropic's app for your computer. It can also run Claude Code sessions on a folder | Free app; Claude Code needs a paid plan |
| Claude Code Remote Control | Approve and steer a Claude Code session from your phone | Included with the plan |
| Agent | An AI that takes actions (files, programs, a browser), not just answers | |
| Chatbot | An AI that answers in a chat. You copy the answer and do the work yourself | Free tiers exist |
| Prompt | What you ask the agent. A good one names the goal, the inputs, the steps, the output, the limits and the check | |
| Git and GitHub | Git keeps a history of every change to your files; GitHub hosts that history online. Optional for the starter kit | Free |
| Python | A programming language. Agents write and run Python scripts for data, files and checks | Free |

## Memory

| Term or tool | What it is | Cost |
|---|---|---|
| `AGENTS.md` | A plain file in the folder telling any agent who you are, how you work and the ground rules. Many agent tools read a file with this name | Free |
| `CLAUDE.md` | The file Claude Code reads every session. Here it's one line pointing to `AGENTS.md`, so you keep one copy. Recent Claude Code reads `AGENTS.md` by itself when there's no `CLAUDE.md`, so the line is a belt-and-braces pointer | Free |
| `RULES.md` | Every decision and correction, numbered, one home each. You teach the agent once | Free |
| `SESSION_HANDOFF.md` | Where you left off and what's next. Chat history runs out; files don't | Free |
| Review rules | Corrections from your reviews, turned into standing rules. My documentation keeps them in a `style.md` (mine, not included) | Free |
| Gotchas | Traps learned the hard way: how a tool really behaves, and the fix | Free |
| Project list (`projects.json`) | One list of every project and where it lives, so an agent can find another project (mine, not included) | Free |
| Vendor memory | Memory built into a chatbot or agent tool. It belongs to that vendor; plain files in your folder belong to you | |

## Hands: the tools the agent drives

| Term or tool | What it is | Cost |
|---|---|---|
| Playwright | Lets the agent drive a real web browser: click, type, take pictures of the screen | Free |
| A separate browser profile | Its own copy of Chrome or Edge, so the agent stays away from your everyday browser and accounts. You sign in yourself | Free |
| DevTools protocol | The browser's built-in remote control, which Playwright uses. It can also save where every element sits, so marks on a picture are computed, not placed by hand | Free |
| python-docx | Lets the agent read and rebuild Word documents by their styles | Free |
| Microsoft Word | Turns the rebuilt draft into a PDF to check every page | Part of Microsoft 365 |
| PyMuPDF | Reads and pictures PDF pages for checks | Free (AGPL license) |
| Pillow | Draws on pictures: boxes, arrows, numbered circles, torn edges | Free |
| Tesseract, RapidOCR, Windows OCR | Read text inside pictures (OCR: optical character recognition). Windows OCR is Windows-only | Free |
| OBS Studio | Records the screen. The agent controls it over a local connection | Free |
| Remotion | Makes video from code: the cursor, click rings, zooms, captions, title cards | Free for individuals and companies up to 3 people; larger companies need a license |
| Adobe Premiere Pro | Video editor. My pipeline builds the project in it, and I review and finish there | Paid: about $22.99 a month (annual plan), $263.88 a year prepaid, or $34.99 a month with no commitment |
| ffmpeg | Cuts, joins and repairs audio and video from the command line | Free |
| Forced aligner (Qwen3-ForcedAligner) | Finds the exact time of every spoken word, for cuts and captions | Free (a graphics card helps) |
| rembg | Cuts an image out of its background | Free |
| YouTube Data API | Uploads videos as private; I publish by hand | Free |
| API | A service's front door for programs, so software can use it without clicking through the website | Varies |
| MCP (Model Context Protocol) | A standard way to plug a tool or service into an agent, like a universal connector | Free standard; the service may charge |

## The team: other AIs

| Term or tool | What it is | Cost |
|---|---|---|
| Subagent | A helper agent the main agent starts for one job, such as a review, with a fresh view | Included with the Claude plan |
| Claude models (Opus, Sonnet, Haiku, Fable) | Anthropic's models: Opus coordinates; others review, play a student, or do quick checks | Included with the Claude plan |
| AI student | A subagent given only screenshots, a mouse and a keyboard, told to follow a manual like a new user and report problems | Included with the plan; my run produced 341 findings, which are leads, not defects |
| Blind second opinion | A different company's model reviews the work without seeing the first review | My spend: about $5.40 for one video's frame review |
| DeepThink | My own small command-line tool that sends a question straight to Google, DeepSeek, Anthropic, OpenAI or Kimi and logs each call's cost. Not published | Each provider bills per call, usually cents |
| OpenRouter | One account and one key for many outside models (Gemini, GPT, image and video models) | Pay per use at provider prices, plus 5.5% when buying credits by card. My spend: about $11.50 for all my video work |
| Gemini, GPT (outside models) | Other companies' models, used for reviews and as extra builders | Pay per use, usually cents to a few dollars a job |
| ElevenLabs | Narration in a clone of your own voice | Paid: Starter $6, Creator $22, Pro $99 a month. A clone of your own voice only |
| edge-tts | A free stock voice for early drafts (not yours) | Free |
| HeyGen | An avatar of you that speaks a script, for intros and outros | Paid: Creator $29 or Pro $49 a month; its API is billed per minute. Optional |
| Abacus.ai | A media service I used by hand for image and video candidates. It has no video API | Paid: from $10 a month. Optional; nothing from it shipped |
| Maker is not the checker | The rule that a different AI (or a person) checks the work, not the one that made it | |

## Boundaries

| Term or tool | What it is | Cost |
|---|---|---|
| Permission prompt | The agent asking "may I?" before it edits a file or runs a command. Claude Code's default | Free |
| Allow-list and deny-list | Settings that pre-approve safe commands and block dangerous ones. They match command text, so they're a seatbelt, not a wall | Free |
| Prompts off | Letting the agent act without asking. Keep the permission prompts on. On my own computer I run with them off and rely on habits instead; that describes my setup, it isn't a recommendation. At work, follow your company's rules. An agent with prompts off can do anything your user account can do | |
| Sandbox | An isolated space (a virtual machine or container) where a program can't reach the rest of your computer or accounts | Varies |
| Secrets store | Where keys live, read at run time, never pasted into a chat or file. I use AWS Secrets Manager; your operating system's keyring works too | AWS: small; keyring: free |
| You sign in | The agent never types a password. You do every sign-in, in its separate browser | Free |
| A person at every step you can't undo | You do every payment, deletion of something the agent didn't create, sending and publishing | Free |
| Review and approve | You set direction, check the work and approve what goes out. Your expertise moves from typing to judging | |
| Prompt injection | Hidden instructions in a web page, email or document that an agent may follow as if they came from you. Not solved | |
| Terms of service | Check a website's terms before an agent automates it. Possible isn't the same as permitted | |

## Where this comes from

The two worked examples have their own repositories, each with its full tool list:
[ai-documentation-pipeline](https://github.com/david-giddyupdata/ai-documentation-pipeline) and
[ai-video-pipeline](https://github.com/david-giddyupdata/ai-video-pipeline). Prices and the "not confirmed" notes are
in [`BEFORE_YOU_START.md`](BEFORE_YOU_START.md).
