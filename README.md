# AI Workspace Blueprints: a starter kit

A chatbot answers. An agent does the work: it opens files, runs programs and hands you something finished to review.
This kit sets up a folder where an AI agent works for you, remembers what you taught it, and stays inside limits you
set. You need no programming. Setup takes about 15 minutes.

By David Baldwin, GiddyUp Data LLC. The takeaway from the talk "Move Beyond the Chatbot" (CSC13, North Texas ISSA,
October 20, 2026).

## Never used GitHub? Start here

You don't need a GitHub account.

1. Do this on your computer, not your phone. On this page, click the green **Code** button, then **Download ZIP**,
   or use this direct link: [download the ZIP](https://github.com/david-giddyupdata/ai-workspace-blueprints/archive/refs/heads/main.zip).
2. Find the ZIP in your Downloads folder and unzip it (Windows: right-click, **Extract All**; Mac: double-click).
   Move the folder somewhere you'll find it again, such as Documents, and rename it if you like.
3. Install **Visual Studio Code** (VS Code), a free editor, from [code.visualstudio.com](https://code.visualstudio.com).
4. In VS Code, open **Extensions** (the four-squares icon on the left), search for **Claude Code** and install the
   extension from Anthropic. Sign in with your Claude account when it asks (Claude Code needs a paid Claude plan; see
   [What it costs](#what-it-costs)).
5. In VS Code, choose **File > Open Folder** and pick the folder you unzipped.
6. Open the Claude Code panel (click the Claude icon at the top right of the editor, or in the left sidebar) and type
   this one sentence:

   > Read START_HERE.md and set this workspace up for me.

The agent asks you a few questions, one at a time, and writes your answers into files it reads every time. It asks
before it creates or changes anything. `START_HERE.md` tells it how; you can read it too.

**Using the Claude desktop app instead?** Start a Claude Code session on the same folder there, and type the same
sentence.

**No editor, or not allowed to install one?** Open
[`use/workspace-blueprint/TUTOR_PROMPT.md`](use/workspace-blueprint/TUTOR_PROMPT.md), copy the prompt into any chatbot
(Claude, ChatGPT, Gemini or similar), then paste in [`use/workspace-blueprint/BLUEPRINT.md`](use/workspace-blueprint/BLUEPRINT.md).
The chatbot coaches you one step at a time.

## What it costs

Claude Code needs a paid Claude plan. The free Claude plan doesn't include it. Prices as of October 2026, from
third-party summaries; check before you buy.

| What | Needed for | Cost |
|---|---|---|
| Claude Code (the agent, inside VS Code or the Claude desktop app) | The setup and everything after it | A paid Claude plan: Pro about $20 a month ($17 a month billed yearly). Heavy use may need Max, $100 or $200 a month |
| Visual Studio Code | The editor that holds the agent, your files and your folder on one screen | Free |
| A chatbot for the tutor prompt | Only if you skip the editor | Free tiers work |

That's all the starter kit needs. Other agent tools can read the same files (see `AGENTS.md` below), so the kit is
not tied to Claude, but the steps here are written for Claude Code. Every tool from the talk, with what it costs, is
in [`GLOSSARY.md`](GLOSSARY.md) and [`BEFORE_YOU_START.md`](BEFORE_YOU_START.md).

## What's in the folder

| File or folder | What it is |
|---|---|
| `START_HERE.md` | Instructions for the agent: interview you, set up the folder, suggest a first project |
| `AGENTS.md` | Who you are, how you work, your ground rules. The setup fills it in. Many agent tools read a file with this name |
| `CLAUDE.md` | One line that tells Claude Code to read `AGENTS.md`. Recent Claude Code reads `AGENTS.md` by itself when there's no `CLAUDE.md`, so this is a belt-and-braces pointer |
| `GLOSSARY.md` | Every tool from the talk in one line each, grouped by the mind map's five branches, with costs |
| `BEFORE_YOU_START.md` | Every tool from the talk with what it costs, and what is Windows-only |
| `mind-map/` | The talk's mind map |
| `use/templates/` | Empty starter files: rules, session handoff, next-session prompt, gotchas, review rules, about me |
| `use/workspace-blueprint/` | A longer step-by-step guide (`BLUEPRINT.md`) and the tutor prompt for any chatbot |
| `use/settings/` | Stricter agent permissions for a company computer, to take to your IT team |
| `use/README.md` | A guide to the `use/` folder, with the key ideas from the talk |
| `SECURITY.md` | How to report a problem privately, and safety basics for using these files |
| `CONTRIBUTING.md` | Issues are welcome; pull requests aren't accepted for now |
| `THIRD_PARTY.md` | The software and services you license yourself |
| `LICENSE` | The MIT License |

## The five branches

The talk's mind map has you and an AI agent, working in one project folder, at the center.

| Branch | What it means |
|---|---|
| **Workspace** | One project folder, open in VS Code, with the agent inside it. The work is files, so it outlives the chat |
| **Memory** | Plain files the agent reads every time: who you are, rules from your corrections, where you left off |
| **Hands** | The tools the agent drives: a browser, files such as Word and images, other programs, connectors |
| **The team** | Other AIs: helper agents, other models, specialist services, and AI checking AI's work |
| **Boundaries** | How much freedom the agent gets, and where a person must step in |

## Two worked examples

Two of my real pipelines, each in its own repository. They are examples to learn from, not software that runs
unmodified on your computer.

- [**ai-documentation-pipeline**](https://github.com/david-giddyupdata/ai-documentation-pipeline): rebuilt a 317-page
  course manual for a changed product screen, captured and annotated the screenshots, and had an "AI student" test
  every exercise.
- [**ai-video-pipeline**](https://github.com/david-giddyupdata/ai-video-pipeline): records a lesson on screen,
  narrates it, edits it and builds the project in Adobe Premiere Pro (a paid subscription).

## Three things to try tomorrow

- Ask for a file, a script or a page instead of an answer.
- Write your next five corrections into a rules file your AI reads every time.
- Have an AI test your instructions the way a brand-new user would. Then check what it finds before you act on it.

## Safety

**Keys and passwords never go in files or chats.** The agent should never ask for them, and you should never paste
them. My own scripts read keys at run time from a secrets manager.

**Keep the permission prompts on.** On my own computer I run with them off and rely on habits instead; that describes
my setup, it isn't a recommendation. At work, follow your company's rules. Claude Code asks before it changes files or
runs commands; say yes when you understand what it's about to do. An agent with prompts off can do anything your user
account can do. At a company, start from [`use/settings/`](use/settings/README.md) and talk to your IT or security
team.

**The agent gets its own browser, and you sign in.** When an agent drives a website, give it a separate browser
profile and do every sign-in yourself. That keeps it away from your other accounts, but once you're signed in it can
act as you on that site.

**A person at every step that can't be undone.** You do every sign-in, payment, deletion of something the agent
didn't create, and publication.

**Prompt injection is not solved.** A web page, email or document can hide instructions, and an agent that reads it
may follow them as if they came from you
([OWASP, LLM01](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)). Keep agents away from data and actions
they don't need, and confirm consequential steps yourself.

## What this is not

- Not a product, and not supported software. It comes with no warranty (see `LICENSE`).
- Not a course, and not security, legal or financial advice.
- Not endorsed by any company whose tools it mentions.

## License and contact

MIT License, copyright 2026 GiddyUp Data LLC: you may use, copy, change and share everything here, including at work,
as long as you keep the copyright and license notice. Third-party tools keep their own licenses
([`THIRD_PARTY.md`](THIRD_PARTY.md)). **The GiddyUp Data name and logo are not licensed for reuse.**

Questions or errors: open an issue on this repository (that one needs a free GitHub account). Don't put keys,
passwords or personal details in an issue; see [`SECURITY.md`](SECURITY.md). Pull requests are not accepted for now
([`CONTRIBUTING.md`](CONTRIBUTING.md)). Training and consulting: [giddyupdata.com](https://giddyupdata.com).
