# For use: copy these, adapt them, use them

Everything in this folder is written to work for anyone, with any agent tool. No programming is needed to start.
The quickest start is one level up: [`../START_HERE.md`](../START_HERE.md) has your agent set up the folder for you.

| Folder or file | What it is | What to do with it |
|---|---|---|
| [`workspace-blueprint/BLUEPRINT.md`](workspace-blueprint/BLUEPRINT.md) | A step-by-step guide to building your own agent environment, in six parts, written for readers with no programming background | Read it, or let a chatbot coach you through it |
| [`workspace-blueprint/TUTOR_PROMPT.md`](workspace-blueprint/TUTOR_PROMPT.md) | A prompt that turns your favorite chatbot (Claude, ChatGPT, Gemini or similar) into a patient coach for the guide, one step at a time | Paste it into the chatbot, then attach or paste `BLUEPRINT.md` |
| [`templates/`](templates/) | Empty starter files: about me, a rules log, a session handoff, a next-session prompt, a gotchas list, review rules | Copy them into your own project folder and fill them in |
| [`settings/`](settings/README.md) | Stricter agent permissions for a company computer, and why an allow-list is not a sandbox | Take it to your IT or security team |

## The six parts of an agent environment

The guide uses six parts: Foundation, Hands, Boundaries, a team of models, Checks, and you as editor. Its table
explains each one
([`workspace-blueprint/BLUEPRINT.md`](workspace-blueprint/BLUEPRINT.md#chatbot-agent-environment-whats-the-difference)).
The talk's mind map groups the same ideas into five branches
([`../README.md`](../README.md#the-five-branches)).

## Key ideas from the talk

The case study: a 317-page course manual (30 exercises, about 360 pictures), rebuilt with AI agents for a changed
product screen in nine working sessions.

1. **Ask for the artifact, not the answer.** An agent reads and writes files, runs tools, drives a browser and calls
   other models. Ask it for the file, the script or the page.
2. **Treat documentation as code.** Keep a master you never edit, and scripts that rebuild the draft from it. A
   change becomes a re-run, not a re-edit.
3. **Start with a template.** Styles make a long document readable for people, editable for agents, and reviewable
   at the level of headings.
4. **Turn every correction into a standing rule.** Keep the rules in a file the agent reads every time. You teach it
   once.
5. **Automate the screen deliberately.** Use a separate browser profile, and sign in yourself.
6. **Test like a newcomer, then verify.** An AI "student" with only screenshots, a mouse and a keyboard walked the
   whole manual overnight. Check its findings before you act on them.
7. **Review what changed, not everything.** Compare against a saved baseline and look only at what changed.
8. **Keep the project's memory in files.** A handoff file, a log of decisions and a next-session prompt. Chat
   history runs out.

## Three things to try tomorrow

They're in the main README: [Three things to try tomorrow](../README.md#three-things-to-try-tomorrow).

## What I do for safety

- I keep API keys in a secrets manager. The agent uses them at run time, and I never paste a key into a chat.
- The agent works in its own browser profile and never types my passwords.
- Destructive actions, such as deleting objects, need my explicit OK, by name.
- The master document is never written; the agent works on a draft.

These are habits and written rules, not a technical barrier. For what a company should add, see
[`settings/README.md`](settings/README.md).

## Where to start

- **New to all of this:** start with [`../START_HERE.md`](../START_HERE.md). Follow the steps in the main README
  ([Never used GitHub? Start here](../README.md#never-used-github-start-here)) and your agent sets up the folder for
  you. No editor? Open [`workspace-blueprint/TUTOR_PROMPT.md`](workspace-blueprint/TUTOR_PROMPT.md) and let a chatbot
  coach you through [`BLUEPRINT.md`](workspace-blueprint/BLUEPRINT.md).
- **Already using an agent tool:** open this folder in it and say "Read START_HERE.md and set this workspace up for
  me", or copy `../AGENTS.md`, `templates/RULES.md` and `templates/SESSION_HANDOFF.md` into one real project and use
  them for a week.
